[//]: # (title: PhpStorm Plugin Development)

<!-- Copyright 2000-2022 JetBrains s.r.o. and other contributors. Use of this source code is governed by the Apache 2.0 license that can be found in the LICENSE file. -->

[PhpStorm](https://www.jetbrains.com/phpstorm/) is an IntelliJ Platform-based product.
Plugins for PhpStorm are developed using the Ultimate Edition of IntelliJ IDEA.

This page describes configuring plugin projects targeting PhpStorm.
See also:
* [PhpStorm Plugin Alternative](plugin_alternatives.md#phpstorm-advanced-metadata)
* [Working with the PHP Open API](php_open_api.md)
* [](existing_plugins.md)

> Please join the dedicated [intellij-php](https://jetbrains-platform.slack.com/archives/C5P9YB0LT/p1653913208725609) Slack channel to discuss PHP related plugin development.
>
{type="tip"}

## Configuring Plugin Projects Targeting PhpStorm

The IntelliJ IDEA Ultimate Edition (with the PHP plugin) must be used for developing PhpStorm plugins because the PHP plugin is incompatible with IntelliJ IDEA Community Edition.
However, this IntelliJ IDEA Ultimate configuration runs the risk of accidentally using some APIs that are not available in PhpStorm.
The recommended best practice is to use PhpStorm for testing.

Configuration of a Gradle-based PhpStorm plugin project is used as a tutorial in the section [Configuring Plugin Projects using the IntelliJ IDEA Product Attribute](dev_alternate_products.md#configuring-plugin-projects-using-the-intellij-idea-product-attribute).
Many techniques are discussed, such as choosing a version of IntelliJ IDEA Ultimate given a targeted version of PhpStorm.

The table below summarizes the [Gradle IntelliJ Plugin](tools_gradle_intellij_plugin.md) attributes to set in the plugin project's Gradle build script.
Click on an entry in the table's *Attribute* column to go to the documentation about that attribute.
To see how these attributes appear in the Gradle build script for PhpStorm, see [](dev_alternate_products.md#configuring-gradle-build-script-using-the-intellij-idea-product-attribute).

| `gradle-intellij-plugin` Attribute                                               | Attribute Value                                                                |
|----------------------------------------------------------------------------------|--------------------------------------------------------------------------------|
| [`intellij.type`](tools_gradle_intellij_plugin.md#configuration-intellij-extension-type)       | `PS` for PhpStorm.                                                             |
| [`intellij.version`](tools_gradle_intellij_plugin.md#configuration-intellij-extension-version) | Set to the targeted `PS` version.                                              |
| [`runIde.ideDir`](tools_gradle_intellij_plugin.md#tasks-runide-idedir)            | Not needed; the Development Instance will automatically match `intellij.type`. |

The PHP plugin version is explicitly declared because it isn't bundled with IntelliJ IDEA Ultimate Edition.
Select a [version](https://plugins.jetbrains.com/plugin/6610-php/versions) of the PHP plugin compatible with the [`intellij.version`](tools_gradle_intellij_plugin.md#configuration-intellij-extension-version).

The dependency on the PHP plugin APIs must be declared in the <path>plugin.xml</path> file, as shown in the tutorial [Configuring plugin.xml](dev_alternate_products.md#configuring-pluginxml) section.
