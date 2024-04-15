Scope: 
- Add `--enableTCP6` flag in all VM Charts
- Make sure this is not repeated twice if also passed in extra args
- Test pod communication via automation

Estimates:
- Changes to all 4 VM charts with UT (considering rework and review) - 4 days
	- Test enabletcp6 flag is passed as args to vm
	- Test enabletcp6 is not duplicated when added in extraargs section
- Manual Validation on IPV6 cluster for all 4 charts - (2 days)
      -  default chart installation should succeed
- Get familiarized with automation framework (3 days)
- Automation changes - 
   - Add network stage to pipeline - 1 day 
   -  Run vm-alert integration feature file in ipv6 only cluster 
   - Complete E2E test - 1 day
- documentation

Add -g in endpoint validation?