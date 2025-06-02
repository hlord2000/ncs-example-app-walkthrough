# A tour of the "ncs-example-application" template, a [Zephyr "T2" project structure](https://docs.zephyrproject.org/latest/develop/west/workspaces.html#t2-star-topology-application-is-the-manifest-repository)

---
* The nRF Connect SDK (NCS) example application is the recommended starting point for serious development (after evaluation).
---
* NCS, by size, is mostly the Zephyr RTOS.
---
* The single "source of truth" for the application is the **[west.yml](https://github.com/nrfconnect/ncs-example-application/blob/main/west.yml)** file. This tells west which version of nRF Connect SDK to use for this project. NCS has another west.yml internally that then pulls in Zephyr/other projects.
---
* West also looks for a file, **[module.yml](https://github.com/nrfconnect/ncs-example-application/blob/main/zephyr/module.yml)** under the **zephyr** directory which explains to the build system where certain additional files are, including (but not limited to) additional **Kconfig files**, **devicetree bindings**, **CMake files**, new **runners** (for flashing). For a full list of arguments allowed in this file, check here: [https://github.com/nrfconnect/sdk-zephyr/blob/666ecc89074c708e71fa0e2f2151cefe617b3606/scripts/zephyr_module.py#L36](https://github.com/nrfconnect/sdk-zephyr/blob/666ecc89074c708e71fa0e2f2151cefe617b3606/scripts/zephyr_module.py#L36)
---
* As mentioned in the title, this application uses the **"T2" or "star" topology**. This means that all dependencies are tracked in the west.yml file per application. If there are a number of products at different places in their life cycle, this makes it easier to pin each to a specific version of the SDK without the difficulty of maintaining forks of every dependency. It may still be worth keeping a fork of nRF Connect SDK if additional changes are needed, however with V3.0, the new **"west patch" command** may make this unnecessary, see the PR here: [https://github.com/zephyrproject-rtos/zephyr/pull/83243](https://github.com/zephyrproject-rtos/zephyr/pull/83243)
---
* The **[Kconfig](https://github.com/nrfconnect/ncs-example-application/blob/main/Kconfig)** file is used to add additional Kconfig files to the project's context and is important for developing Zephyric drivers and configuring libraries in a clean way. The **"rsource" command** here is just a "relative source", basically like an include in Make. [https://docs.zephyrproject.org/latest/build/kconfig/extensions.html](https://docs.zephyrproject.org/latest/build/kconfig/extensions.html)
---
* The root **[CMakeLists.txt](https://github.com/nrfconnect/ncs-example-application/blob/main/CMakeLists.txt)** file adds sources for drivers and libraries but does not contain the required command for making a Zephyr project build properly. This command is in the **[app/CMakeLists.txt](https://github.com/nrfconnect/ncs-example-application/blob/main/app/CMakeLists.txt)** file where application specific source and header files are also selected.
---
* Also be sure to take a look at the **[.github/workflows](https://github.com/nrfconnect/ncs-example-application/tree/main/.github/workflows)** files for examples on how to build applications and docs in CI (GitHub in example, but basic flow applies to other runners).
---
* The **[boards](https://github.com/nrfconnect/ncs-example-application/tree/main/boards)** directory is where custom boards should be created. In **[app/boards](https://github.com/nrfconnect/ncs-example-application/tree/main/app/boards)** specific application overrides can be made.
---
* The **[dts/bindings](https://github.com/nrfconnect/ncs-example-application/tree/main/dts/bindings)** directory is used to create new devicetree bindings for your application. Devicetree bindings can also be places in board specific folders.
---
* For more information on an application's structure, be sure to check out Nordic's DevAcademy courses here: [https://academy.nordicsemi.com/](https://academy.nordicsemi.com/)
