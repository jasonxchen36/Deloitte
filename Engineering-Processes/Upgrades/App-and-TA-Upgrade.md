1. Take inventory of apps in dev, stage and production
2. Check in splunkbase to verify if there is an updated version of deployed apps. If there is an upgraded app, read through documentation and understand differences between outdated and updated app and potential impacts
3. Review configurations in default for potential conflicts/breakage of outdated app. i.e. default field extractions/aliases that was decommissioned in upgraded app
4. Take backup of apps in dev that are going to be updated 
5. Deploy updated apps in dev
6. Perform dev validation. Confirm for any former changes.  
7. Take backup of apps in stage that are going to be updated 
8. Deploy updated apps in stage via a DevOps pull request 
9. Perform stage validation
10. Take backup of apps in prod that are going to be updated  
11. Deploy updated apps in prod via a DevOps pull request 
12. Perform prod validation


Future Enhancement Process to be developed
- Quarterly app upgrade
- Ongoing app upgrade
