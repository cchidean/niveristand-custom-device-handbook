### When do you Need a Custom Device?

VeriStand provides the general functionality required by most real-time (RT) testing applications. However, NI has designed the VeriStand environment to be customizable to meet any additional application requirements.

The built-in components of a VeriStand Project are listed in the *VeriStand Help* topic [VeriStand Environment](https://www.ni.com/documentation/en/veristand/latest/manual/environment/). If these components do not fulfill your specifications, try one of the customization methods in [Using NI VeriStand with Other Software Environments to Create Real-Time Test Applications](https://www.ni.com/en-us/innovations/white-papers/09/using-ni-veristand-with-other-software-environments-to-create-re.html).

There is a collection of [VeriStand add-ons](https://www.ni.com/en-us/support/documentation/supplemental/15/veristand-add-ons.html) that have been gathered from internal NI developers and the VeriStand community. You should check for an existing custom device before building one.

There are three specifications that are best-suited for a custom device.
1.	3rd Party Hardware
2.	Unsupported Measurement or Generation Mode
3.	Feature

#### 3rd Party Hardware

Determine if your hardware is natively supported by VeriStand. For more information, refer to the *VeriStand Help* topic [NI Hardware Support](https://www.ni.com/documentation/en/veristand/latest/manual/ni-hardware-support/). If your application requires other hardware, it can be implemented in a custom device.

**Note:** Several hardware vendors have created custom devices for their hardware. Contact the manufacturer before building a custom device.

#### Unsupported Measurement or Generation Mode

Determine if the required measurement or generation mode of your hardware is supported. For more information, refer to the *VeriStand Help* topic [Adding and Configuring Hardware Devices](https://www.ni.com/documentation/en/veristand/latest/manual/add-configure-hardware-device/).

If not supported, it can be implemented in a custom device. For example, single-point hardware-timed analog acquisition on NI-DAQ devices is supported in VeriStand. Continuous analog acquisition can be implemented as a custom device.

#### Feature

Determine if VeriStand's built-in functionality meets your needs. Most RT testing application features, such as host interface communication, data logging, and stimulus generation, are provided.

If a required feature is not built-in, it can be implemented by extending VeriStand. For a list of ways to customize VeriStand, refer to [Using NI VeriStand with Other Software Environments to Create Real-Time Test Applications](https://www.ni.com/en-us/innovations/white-papers/09/using-ni-veristand-with-other-software-environments-to-create-re.html)

Certain features are best implemented as custom devices. To determine when a custom device is the most appropriate mechanism to meet a specification, you should be familiar with all the customization methods available. A general rule is that custom devices implement features that require or use VeriStand channel data on the execution host.

For example, a [TDMS File Viewer](https://www.ni.com/documentation/en/veristand/latest/manual/enhance-workspace-tools/) is built into the VeriStand Workspace. If you need to log VeriStand channels to TDMS without first sending it back to the Workspace (as with high-speed streaming), a custom device called the [Embedded Data Logger](https://www.ni.com/documentation/en/veristand/latest/manual/log-target-data-embedded-data-logger/) fulfills this requirement.

If you need to display previous test results on the workspace while a new test is running, a custom workspace object may be more appropriate. For more information, refer to [Creating Custom Workspace Objects for VeriStand](https://knowledge.ni.com/KnowledgeArticleDetails?id=kA03q000000x4QfCAI&l=en-US).

#### Custom Device Risk Analysis

The open nature of VeriStand is a strong advantage over other RT/HIL testing solutions. You can take advantage of this extensibility by using custom devices written by other developers. Writing your own custom device incurs a set of manageable risks. This section provides a list of risks that should be considered before custom device development begins.

#### LabVIEW Application Development

Custom devices are written in LabVIEW. The framework generated by the [NI VeriStand Custom Device Wizard](https://github.com/ni/niveristand-custom-device-wizard) is single-loop or an action-engine VI. This architecture may be suitable for simple custom devices. Advanced custom devices will require more complicated architecture.

A prerequisite for custom device development is thorough knowledge of LabVIEW programming and application architectures. This knowledge represents [NI Certified LabVIEW Developer](https://education.ni.com/badges/resources/1255) (CLD) level expertise. You can obtain this experience through [NI's Training and Certification](https://www.ni.com/en-us/shop/services/education-services.html) program by completing the LabVIEW [Core 1](https://www.ni.com/en-us/shop/services/education-services/customer-education-courses/labview-core-1-course-overview.html), [Core 2](https://www.ni.com/en-us/shop/services/education-services/customer-education-courses/labview-core-2-course-overview.html), and [Core 3](https://www.ni.com/en-us/shop/services/education-services/customer-education-courses/labview-core-3-course-overview.html) courses.

VeriStand custom devices are typically not large LabVIEW applications. Custom devices are designed to be modular, self-contained add-ons that add a specific functionality to VeriStand. While custom devices are typically developed by a single programmer, large application development best-practices may still apply. For more information, refer to the *LabVIEW Help* topic [Best Practices for Large Application Development](https://zone.ni.com/reference/en-XX/help/371361R-01/lvdevconcepts/best_practices_large_apps/).

#### LabVIEW RT Application Development

Custom devices are typically designed to execute on RT systems. This allows the operator to perform deterministic HIL and RT test procedures.

Programming for an RT system requires knowledge of real-time operating systems (RTOS) and specialized LabVIEW development techniques. This knowledge is typically obtained through [NI's Training and Certification](https://www.ni.com/en-us/shop/services/education-services.html) program by completing the [Real-Time Application Development](https://www.ni.com/en-us/shop/services/products/labview-real-time-1-course.html) course and refined by working on several LabVIEW RT applications.

#### VeriStand Background

Familiarity with the VeriStand Engine is crucial to successful custom device development. Selecting the appropriate type in the Custom Device Template Tool is difficult without understanding each type. For more information, refer to the *VeriStand Help* and the [Understanding the VeriStand Engine](https://www.ni.com/documentation/en/veristand/latest/manual/vs-engine/) topic.

Experience with VeriStand from an operator's perspective is helpful. This experience enables you to build operator-friendly interfaces that conform to the standard look and feel of other VeriStand components. Familiarity with VeriStand allows the developer to build a complex system definition, which allows thorough testing and benchmarking.

#### Hardware Driver Development

The custom device must call a hardware or instrument driver to support 3rd-party hardware. All NI hardware comes with a LabVIEW Application Program Interface (API) that can be used in the custom device. However, just because a LabVIEW API exists does not guarantee the custom device can be easily implemented.

Consider the following points when evaluating the feasibility of a custom device for 3rd-party hardware.

1. Does an Instrument Driver exist? For more information, refer to [Instrument Driver Network](https://www.ni.com/en-us/support/downloads/instrument-drivers.html).
2. Is a hardware driver available?
3. Is the driver well documented?
4. Can the hardware requirement be met by passing LabVIEW double data type (DBLs) to and from the custom device during steady state operation?

VeriStand uses channels to pass data between different parts of the system, including to and from custom devices. All VeriStand channels are LabVIEW DBLs. For more information on LabVIEW data types, refer to the *LabVIEW Help* topic [Floating Point Numbers](https://zone.ni.com/reference/en-XX/help/371361R-01/lvhowto/floating_point_numbers/).

If the hardware driver returns a vector, structure, or any non-DBL data, that information cannot be passed directly from the custom device to the rest of the VeriStand system. The developer is responsible for finding a way to pass data. For more information on available communication mechanisms, refer to the *LabVIEW Real-Time Module Help* topic [Exploring Remote Communication Methods](https://zone.ni.com/reference/en-XX/help/370715P-01/lvrtconcepts/exploring_communication_methods/).

VeriStand also exposes its TCP pipe through dynamic event registration. This pipe may suite your remote communication requirements. for more information, refer to Custom Device Engine Events section.

#### Testing

A custom device is one part of a VeriStand system. The complete state of the operator's system is seldom known by the custom device developer. System state includes the following information.

1. Target and host computer specifications.
2. System definition components.
3. Computational intensity of the simulation models.
4. Required loop rates.
5. System health and resource utilization.

Ideally, the custom device is implemented to be minimally burdensome, extremely efficient, and easy to use. Depending on complexity, it may become necessary to test, debug, and optimize the code on systems representative of the operator’s system.

Consider the following example. A custom device developer needs to benchmark a 3rd-party hardware custom device. They add the custom device to the VeriStand Engine Demo and deploy the system definition to a quad-core PXIe-8880 Controller. Adding the custom device to the system increased the target’s CPU load by 10% per-core and RAM utilization by 120KB.

If the operator is deploying the same custom device to a single-core PXIe-8821 Controller, with an average CPU load of 60% because of a computationally intense model, it’s unlikely the operator will achieve the same loop rate. Their system may be incapable of running the custom device at all.

Time to test, debug and optimize the code must be factored into the development timeline. If you are developing for a specific operator, test on a representative system. If you are developing for unknown systems, include the benchmarked system specifications and timing information with the custom device documentation.
