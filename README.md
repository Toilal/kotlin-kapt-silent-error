###  Error:Execution failed for task ':app:kaptDebugKotlin'

This configuration cause a compilation error when running gradle build that is perfectly fine.

```
gradlew build
...
app\build\tmp\kapt3\stubs\debug\dummy\myapplication\MainActivity.java:3: 
error: org.androidannotations.annotations.EActivity cannot be used on a final element
...
```

That's because class must be declared `open` for EActivity annotation to work properly.

### IntelliJ Issue

But when running in IntelliJ with Android Plugin, only a cryptic error appears and real error message is not accessible.

```
Error:Execution failed for task ':app:kaptDebugKotlin'.
> Internal compiler error. See log for more details
```

it's not possible to read the effective compilation error message, neither from UI or idea logs.

`idea.log` contains the following stacktrace instead.

```
java.lang.NoSuchMethodException: com.android.ide.common.blame.Message.<init>(com.android.ide.common.blame.Message$Kind, java.lang.String, java.lang.String, com.google.common.collect.ImmutableList)
	at java.lang.Class.getConstructor0(Class.java:3082)
	at java.lang.Class.getConstructor(Class.java:1825)
	at org.jetbrains.kotlin.android.KotlinOutputParserHelper$simpleMessageConstructor$2.invoke(KotlinOutputParserHelper.kt:171)
	at org.jetbrains.kotlin.android.KotlinOutputParserHelper$simpleMessageConstructor$2.invoke(KotlinOutputParserHelper.kt:143)
	at kotlin.SynchronizedLazyImpl.getValue(Lazy.kt:130)
	at org.jetbrains.kotlin.android.KotlinOutputParserHelper.getSimpleMessageConstructor(KotlinOutputParserHelper.kt)
	at org.jetbrains.kotlin.android.KotlinOutputParserHelper.createNewMessage(KotlinOutputParserHelper.kt:272)
	at org.jetbrains.kotlin.android.KotlinOutputParserHelper.createMessage(KotlinOutputParserHelper.kt:250)
	at org.jetbrains.kotlin.android.KotlinOutputParserHelper.createMessage$default(KotlinOutputParserHelper.kt:244)
	at org.jetbrains.kotlin.android.KotlinOutputParserHelperKt.parse(KotlinOutputParserHelper.kt:41)
	at org.jetbrains.kotlin.android.KotlinOutputParser.parse(KotlinOutputParser.java:28)
	at com.android.ide.common.blame.parser.ToolOutputParser.parseToolOutput(ToolOutputParser.java:86)
	at com.android.tools.idea.gradle.output.parser.BuildOutputParser.parseGradleOutput(BuildOutputParser.java:43)
	at com.android.tools.idea.gradle.project.build.invoker.GradleTasksExecutor$GradleTasksExecutorImpl.lambda$collectMessages$5(GradleTasksExecutor.java:517)
	at com.intellij.openapi.application.impl.ApplicationImpl$2.run(ApplicationImpl.java:342)
	at java.util.concurrent.Executors$RunnableAdapter.call(Executors.java:511)
	at java.util.concurrent.FutureTask.run(FutureTask.java:266)
	at java.util.concurrent.ThreadPoolExecutor.runWorker(ThreadPoolExecutor.java:1142)
	at java.util.concurrent.ThreadPoolExecutor$Worker.run(ThreadPoolExecutor.java:617)
	at java.lang.Thread.run(Thread.java:745)
```