Scope: 
- Add `--enableTCP6` flag in all VM Charts
- Make sure this is not repeated twice if also passed in extra args
- Test pod communication via automation

Estimates:
- Changes to all 4 VM charts with UT (considering rework and review) - 
	- Add and test enabletcp6 flag is passed as args to vm - **2 days**
	- Test enabletcp6 is not duplicated when added in extraargs section  - **2 days**
- Manual Validation on IPV6 cluster for all 4 charts - 
      -  default chart installation should succeed - **2 days**
- Get familiarized with automation framework - **3 days**
- Automation changes - 
   - Add new feature files to validate
	   - choose ipv6 in nuke cluster creation (IPV6 cluster and multiple replicas)
	   - default chart installation for all 4 charts in ipv6  - **4 days**
	   - Integration validation where all vm components, cpro  come up in ipv6  - **3 days**
	   - Debug any functional issues - 3 days
- Monitor pipeline after all changes - **1 day**

Total : 20 days

