[//]: # (title: Notable Changes in IntelliJ Platform and Plugins API 2021.*)

<!-- Copyright 2000-2021 JetBrains s.r.o. and other contributors. Use of this source code is governed by the Apache 2.0 license that can be found in the LICENSE file. -->

## 2021.2

### Notable Changes in IntelliJ Platform 2021.2
       
Unit test mode: non-production `IconManager`        
: Now `com.intellij.ui.IconManager.createDeferredIcon()` doesn't use `iconProducer` which might result in "wrong" composite icons and failed assertions. Override `UsefulTestCase.isIconRequired()` returning `true` to restore production icons. Alternatively, invoke `Registry.get("psi.deferIconLoading").setValue(false)` in `setUp()` and `Registry.get("psi.deferIconLoading").resetToDefault()` in `tearDown()`.
                     
Constructor Injection disabled for Extensions
: Please obtain necessary components only when needed (logged as ERROR now).

## 2021.1

### Notable Changes in IntelliJ Platform 2021.1

_Add unambiguous imports on the fly_ for custom languages
: Override [`ReferenceImporter#isAddUnambiguousImportsOnTheFlyEnabled()`](upsource:///platform/analysis-impl/src/com/intellij/codeInsight/daemon/ReferenceImporter.java) and provide corresponding user setting. Implement `HintAction` with `fixSilently()` and hook it up to highlighting as a quick fix for unresolved reference.
                                    
Ability to override encoding per `VirtualFile`
: Implement [`FileEncodingProvider`](upsource:///platform/core-api/src/com/intellij/openapi/vfs/encoding/FileEncodingProvider.java) and register in `com.intellij.fileEncodingProvider` extension point.
                                                                         
[JCEF](jcef.md): wrapper for `CefBrowser` 
: [`JBCefOsrHandlerBrowser`](upsource:///platform/platform-api/src/com/intellij/ui/jcef/JBCefOsrHandlerBrowser.java) forwards to custom `CefRenderHandler`, e.g., for off-screen rendering.

### Notable Changes in Java Plugin 2021.1

Testframework: JUnit4 variant for `LightJavaCodeInsightFixtureTestCase`
: Use `com.intellij.testFramework.fixtures.LightJavaCodeInsightFixtureTestCase4`.