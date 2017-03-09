===========
Description
===========

Tool for testing upgrades of the OpenStack software. The tool validates if an OpenStack deployment can perform an upgrade of its services 
from one release N-1 to a release N successfully, or from the latest official release to master. It also provides information that can be 
used to assess if an upgrade complies with the requirements for being recognized as a **rolling upgrade**, a **zero downtime upgrade** or a 
**zero impact upgrade**.

|

============
Requirements
============

**Functional**

- The tool *must* be agnostic to the OpenStack environment and the deployment tool used, performing actions consistently across different environments
- It *could* validate that after an upgrade, services are actually at the correct release version
- It *must* validate that after an upgrade, all services are still functional
- It *must* validate that existing resources, like VMs or volumes, are not affected by the upgrade
- It *must* be capable of measuring if there is API downtime during the upgrade for any of the supported services listed below
- It *should* verify that all requests made during an upgrade are honored at some point successfully, validating that they are not just added to the queue but are actually processed at some point
- It *must* be capable to detect if any of the supported services listed below is not fully available at some point during the upgrade
- It *must* be capable of measuring the performance of the supported services listed below, before, during, and after an upgrade
- It *must* have a centralized store for logs of tests and data collected during an upgrade
- It *must* attempt to clean up after itself, if resources were created for testing or monitoring purposes they must be removed after the upgrade finishes 
- It *must* be scalable in services meaning that when new services are ready to implement an upgrade strategy (for example zero downtime or zero impact), they can be easily added to the scope of the tool
- It *could* include a GUI where results can be easily interpreted and should include trends
- It *must* provide a common public interface that can be used to communicate with and from deployment tools so certain steps of the deployment or the upgrade can be triggered
- It *could* provide the capability to add tests via a plugin system 

**Non-Functional**

- *Must* be python 3 compatible
- *Must* be compatible with Linux environments
- *Should* be an official OpenStack project

**Supported Services**

- Authentication
- Compute
- Object Storage

|

=====================
Requirements priority
=====================

Must have
  Requirements labeled as Must have are critical to the current delivery timebox in order for it to be a success. If even one Must have 
  requirement is not included, the project delivery should be considered a failure (note: requirements can be downgraded from Must have, 
  by agreement with all relevant stakeholders; for example, when new requirements are deemed more important).

Should have
  Requirements labeled as Should have are important but not necessary for delivery in the current delivery timebox. While 'Should have' 
  requirements can be as important as 'Must have', they are often not as time-critical or there may be another way to satisfy the 
  requirement, so that it can be held back until a future delivery timebox.

Could have
  Requirements labeled as Could have are desirable but not necessary, and could improve user experience or customer satisfaction for 
  little development cost. These will typically be included if time and resources permit.

Won't have
  Requirements labeled as Won't have have been agreed by stakeholders as the least-critical, lowest-payback items, or not appropriate 
  at that time. As a result, 'Won't have' requirements are not planned into the schedule for the delivery timebox. 'Won't have' 
  requirements are either dropped or reconsidered for inclusion in later timeboxes.
  
|

============
Main modules
============

- Data store
- Data parser
- Test manager
- Release version validator* (Lower priority)
- System health validator
- Persistent resources validator
- API uptime monitor
- Service availability monitor
- Service performance monitor
- External tests plugin system
- Deployment control interface 
- Report generator
