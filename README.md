# t12-t245-controllers-docs

# Table of Contents
* [Where is Open Firmware](#Where-is-Open-Firmware)
	* [STM32 based - For KSGER T12 OLED or QUICK](#STM32-based---For-KSGER-T12-OLED-or-QUICK)
	* [MM32SPIN27 based - For T12-958 soldering station](#MM32SPIN27-based---For-T12-958-soldering-station)
* [Where is Docs for how to install Open Firmware](#Where-is-Docs-for-how-to-install-Open-Firmware)
* [Where are schematics photos etc for my KSGER Station](#Where-are-schematics-photos-etc-for-my-KSGER-Station)
* [Introduction](#Introduction)
* [Sections](#Sections)
	* [Controllers](#Controllers)
	* [Tips and Handles](#Tips-and-Handles)
	* [Tools](#Tools)
	* [Research](#Research)
* [Disclaimers](#Disclaimers)
	* [Organisation and Navigation](#Organisation-and-Navigation)
	* [Copyright and Attribution](#Copyright-and-Attribution)
	* [Mirrors](#Mirrors)


Mirrors and research repository documenting a variety of soldering iron controllers for t12, t245, and more!

## Where is Open Firmware

### STM32 based - For KSGER T12 OLED or QUICK

* Looking for Open Source Firmware, to Flash on to KSGER / T12 OLED Station?

Here it is:

* [Newest Source Code](https://github.com/deividAlfa/stm32_soldering_iron_controller) by DavidAlpha.
* Based of PTDreamer's source code for the `v1.5` hardware. It was then extensively updated by DavidAlpha.
* Thanks DavidAlpha!

### MM32SPIN27 based - For T12-958 soldering station

* Looking for Open Source Firmware, to Flash on to T12-958 soldering station?

Here it is:

* [Main repo](https://github.com/koendv/t12-958)
* Created by @koendv, for boards with MindMotion MM32SPIN27 mcu

<a id="where-is-docs-for-how-to-install-open-firmware"></a>
## Where is Docs for how to install Open Firmware

Same place as the source code:

* [Newest Source Code](https://github.com/deividAlfa/stm32_soldering_iron_controller) by DavidAlpha.
* Thanks DavidAlpha!


<a id="but-where-are-schematics-photos-etc-for-my-ksger-station"></a>
## Where are schematics photos etc for my KSGER Station

For most new visitors, you will find them here under the [`controllers` folder](https://github.com/dreamcat4/t12-t245-controllers-docs/tree/master/controllers/stm32-t12-oled)

<a id="introduction"></a>
## Introduction

It is sometimes difficult to find technical information. And sometimes that information is strewn all around the web. It would seem without any thought to a consistent or logical organization.

This repository provides research and technical information about soldering irons and their associated platforms. Or it provides external links to where you can such information.

* STM32 T12 OLED Soldering Iron Controllers, made by 'QUICK' or 'KEGER', or 'WOKA', or unbranded
* A variety of different Open Source Soldering Iron Controller projects
* Open Source Firmware for a few specific Soldering Iron Controllers
* Hakko T12 or T15 tips / handles / cartridges (or clones thereof)
* T245 (aka C245) tips / handles / cartridges
* T210 (aka C210) tips / handles / cartridges
* Schematics, wiring diagrams, and other technical characteriztions
* Where to find forum theads and public discussions about these things

<a id="sections"></a>
## Sections

<a id="controllers"></a>
### Controllers

For [controllers](controllers) identified to be of particular interest. Some have known PCB revisions, and schematics.

<a id="tips-and-handles"></a>
### Tips and Handles

Documentation for different Soldering Iron [Tips or Handles](tips-and-handles).

<a id="tools"></a>
### Tools

[Hardware and software tools](tools) which help to support: device programming, debugging, or external calibration of the soldering iron.

<a id="research"></a>
### Research

[Research materials](research) which do not neatly fall into the above categories. They may include significant information for multiple different categories. Or if written in a foreign language, then a translation to english is provided.

<a id="disclaimers"></a>
## Disclaimers

This is a repository of information collected from around the web. To facilitate the finding of this frequently sought after information. To help aid navigation, most sources have been organized into a logical folder structure. Which is loosely based around the families of hardware to which they belong to. However some information sources a relevant to multiple different families of hardware. These are then dumped into a 'general' category. Or something like that.

Whatever documentation you find here is provided 'as is'. Source materials have not been vetted or cross checked for their validity. So specific technical details may either be in error, or otherwise not specific enough to all variations of a hardware or software they are describing. So use at your own risk.

However if you do manage to spot an error. And feel that you can suggest an improvement to help better organise this documentation. Then please put together a Pull Request, or Open a new issue, and put forward those ammendments. Such corrections and improvements are most welcome.

<a id="organisation--navigation"></a>
### Organisation and Navigation

Usually you will start in a parent folder by reading it's README.md. Which describes what is inside that specific folder. Then by clicking or navigating into subfolders, they will very often have their own more specific README.md file. With more details and / or links to elswhere.

Many of the subfolders 'further down' will also include those relevant gathered research documents, schematics, etc. Which are specific to that particular model of the hardware. But when it is unclear which variant of the hardware the schematic is referring to... then it may instead be located in a parent folder. With infos about specific sub-variant(s) shoved into their own subfolders underneath that.

<a id="copyright-and-attribution"></a>
### Copyright and Attribution

All copyrighted or trademarked materials remain the property of their respective owners. And no attempts are being made to try to disguise that. However in many cases it's not easy to provide a clear or correct attribution. This occurs when the information source has no copyright notice, licensing or attribution provided along with it. It is therefore difficult for me to identify legitimate copyright or attribution calims on such works. However for the vast majority cases it appears to be because the author has freely chosen to put their work into the public domain. For usage without restriction. If you are genuinely a source of anything being provided here, and would either like to have a better attribution, wish to suggest a modification, correction, or otherwise wish to assert any form of copyright claim: Then in the first instance the suggestion is to please open up an issue here on github. So that the matter may be publically discussed and debated out in the open. Should you wish to raise an issue by email. Then that email will simply be copied [in full] as a new open issue, onto the github issues tracker. So that it can then be publically discussed. The exception to this is the situation whereby I am contacted specifically for the purpose of removing an existing attribution. In which case your email request will be kept private. This repository of information is provided merely for the benefit of the broader community and the general public. Therefore (likewise) we are happy to discuss these matters publically. It is most fitting. Thank you for your understanding.

<a id="mirrors"></a>
### Mirrors

In order to preserve fully the context and the source of the information being provided. Some information sources are provided here as a website mirror. This is either for an archival purpose, should the source become inaccessible in the future. Or to provide an appropriate English Language translation of the source material(s). Which was essential processing step in order to disseminate those information sources. Otherwise those materials would not be an a browsable format. And their contribution would have been missed. Just like all of the other source materials gathered here, a mirrored information source is considered to remain under the ownership of it's respective copyright and trademark holder(s). And therefore subject to the same terms per the previous section.