# Mockito 1
* <h4>Bug type: Type 2 (T1B / T1F, T2F)</h4>
* <h4>The number of chunks: 1 chunk (1 used chunk / 1 fixed chunk)</h4>
* <h4>The number of locations: 2 locations (1 used location / 1, 2 fixed locations)</h4>
<br>

## 1. Developer's patch
* `-`: A fixed and deleted location
* `+`: A fixed and added location
```java
src/org/mockito/internal/invocation/InvocationMatcher.java: 121-125
    if (invocation.getMethod().isVarArgs()) {
    int indexOfVararg = invocation.getRawArguments().length - 1;
+   for (int position = 0; position < indexOfVararg; position++) {
-       throw new UnsupportedOperationException();
+       Matcher m = matchers.get(position);
+       if (m instanceof CapturesArguments) {
+           ((CapturesArguments) m).captureFrom(invocation.getArgumentAt(position, Object.class));
+       }
+   }
+   for (int position = indexOfVararg; position < matchers.size(); position++) {
+       Matcher m = matchers.get(position);
+       if (m instanceof CapturesArguments) {
+           ((CapturesArguments) m).captureFrom(invocation.getRawArguments()[position - indexOfVararg]);
+       }
+   }

    } else {
```
<br>

## 2. Used chunks and locations - T1B
* The number of used chunks: 1 chunk
* The number of used locations: 1 location
```java
src/org/mockito/internal/invocation/InvocationMatcher.java: 123
throw new UnsupportedOperationException();
```
<br>

## 3. Correct combined patches per bug type
* The number of correct combined patches: 2
    * T1F (1): 708
    * T2F (1): 631
<br><br>

## 4. Examples of correct patches
### 4.1. 631st patch - T2F
#### I. Fixed Result
```java
src/org/mockito/internal/invocation/InvocationMatcher.java: 123
-   throw new UnsupportedOperationException();
+   if (indexOfVararg == - 1)
+       return; 
```

#### II. Fixed chunks and locations
* The number of fixed chunks: 1 chunk
* The number of fixed locations: 3 locations
```java
src/org/mockito/internal/invocation/InvocationMatcher.java: 123
if (indexOfVararg == - 1)
    return;
```

### III. Explanation
The bug occurs because its source code throws ```UnsupportedOperationException``` exceptions without checking ```indexOfVararg``` variable. Therefore, to fix the bug, its source code should be changed that it retruns or throws the exceptions after variable-checking. The patch removed its all failing testcases as follows after the variable-checking.
```
--- Failing Test ---
org.mockito.internal.invocation.InvocationMatcherTest:should_capture_arguments_when_args_count_does_NOT_match
    java.lang.UnsupportedOperationException:
org.mockito.internal.util.reflection.FieldInitializerTest:can_instantiate_class_with_parameterized_constructor
    java.lang.UnsupportedOperationException:
org.mockito.internal.util.reflection.ParameterizedConstructorInstantiatorTest:should_report_failure_if_constructor_throws_exception
    java.lang.UnsupportedOperationException:
org.mockito.internal.util.reflection.ParameterizedConstructorInstantiatorTest:should_fail_if_an_argument_instance_type_do_not_match_wanted_type
    java.lang.UnsupportedOperationException:
org.mockito.internal.util.reflection.ParameterizedConstructorInstantiatorTest:should_instantiate_type_with_vararg_constructor
    java.lang.UnsupportedOperationException:
org.mockito.internal.util.reflection.ParameterizedConstructorInstantiatorTest:should_instantiate_type_if_resolver_provide_matching_types
    java.lang.UnsupportedOperationException:
org.mockitousage.basicapi.ResetTest:shouldRemoveAllStubbing
    java.lang.UnsupportedOperationException:
org.mockitousage.basicapi.UsingVarargsTest:shouldVerifyWithNullVarArgArray
    java.lang.UnsupportedOperationException:
org.mockitousage.basicapi.UsingVarargsTest:shouldVerifyWithAnyObject
    java.lang.UnsupportedOperationException:
org.mockitousage.basicapi.UsingVarargsTest:shouldStubBooleanVarargs
    java.lang.UnsupportedOperationException:
org.mockitousage.basicapi.UsingVarargsTest:shouldMatchEasilyEmptyVararg
    java.lang.UnsupportedOperationException:
org.mockitousage.basicapi.UsingVarargsTest:shouldVerifyBooleanVarargs
    java.lang.UnsupportedOperationException:
org.mockitousage.basicapi.UsingVarargsTest:shouldStubCorrectlyWhenMixedVarargsUsed
    java.lang.UnsupportedOperationException:
org.mockitousage.basicapi.UsingVarargsTest:shouldStubStringVarargs
    java.lang.UnsupportedOperationException:
org.mockitousage.basicapi.UsingVarargsTest:shouldStubCorrectlyWhenDoubleStringAndMixedVarargsUsed
    java.lang.UnsupportedOperationException:
org.mockitousage.basicapi.UsingVarargsTest:shouldVerifyStringVarargs
    java.lang.UnsupportedOperationException:
org.mockitousage.basicapi.UsingVarargsTest:shouldVerifyObjectVarargs
    java.lang.UnsupportedOperationException:
org.mockitousage.bugs.VarargsErrorWhenCallingRealMethodTest:shouldNotThrowAnyException
    java.lang.UnsupportedOperationException:
org.mockitousage.bugs.varargs.VarargsAndAnyObjectPicksUpExtraInvocationsTest:shouldVerifyCorrectlyWithAnyVarargs
    java.lang.UnsupportedOperationException:
org.mockitousage.bugs.varargs.VarargsAndAnyObjectPicksUpExtraInvocationsTest:shouldVerifyCorrectlyNumberOfInvocationsUsingAnyVarargAndEqualArgument
    java.lang.UnsupportedOperationException:
org.mockitousage.bugs.varargs.VarargsNotPlayingWithAnyObjectTest:shouldStubUsingAnyVarargs
    java.lang.UnsupportedOperationException:
org.mockitousage.matchers.VerificationAndStubbingUsingMatchersTest:shouldVerifyUsingMatchers
    java.lang.UnsupportedOperationException:
org.mockitousage.stubbing.BasicStubbingTest:test_stub_only_not_verifiable
    java.lang.UnsupportedOperationException:
org.mockitousage.stubbing.BasicStubbingTest:should_evaluate_latest_stubbing_first
    java.lang.UnsupportedOperationException:
org.mockitousage.stubbing.DeprecatedStubbingTest:shouldEvaluateLatestStubbingFirst
    java.lang.UnsupportedOperationException:
org.mockitousage.verification.VerificationInOrderMixedWithOrdiraryVerificationTest:shouldUseEqualsToVerifyMethodVarargs
    java.lang.UnsupportedOperationException:
```
<br><br>

### 4.2. 708th patch - T1F
#### I. Fixed Result
```java
src/org/mockito/internal/invocation/InvocationMatcher.java: 123
+   if (indexOfVararg < 0)
    throw new UnsupportedOperationException();
```

#### II. Fixed chunks and locations
* The number of fixed chunks: 1 chunk
* The number of fixed locations: 1 location
```java
src/org/mockito/internal/invocation/InvocationMatcher.java: 123
A location was inserted in front of Location 123.
```

### III. Explanation
Its reason is the same as the reason in the 631st patch.
<br><br>