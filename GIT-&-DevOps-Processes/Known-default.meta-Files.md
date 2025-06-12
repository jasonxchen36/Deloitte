Our automated build script checks committed default.meta files against a whitelist of known configurations.  

Please use one of these configurations for newly created apps. If you need a custom default.meta, you may submit it for manual review in your PR.
#For SHC Applications
##General default.meta: 
[]
access = read : [ admin, sc_admin, cpblty_gems_user ], write : [ admin, sc_admin, cpblty_gems_admin ]
export = system
owner = nobody

####OR 
[]
access = read : [ admin, sc_admin, cpblty_gems_es_user ], write : [ admin, sc_admin, cpblty_gems_admin ]
export = system
owner = nobody

####OR 

[]
access = read : [ admin, sc_admin, cpblty_gems_es_user ], write : [ admin, sc_admin, cpblty_gems_admin ]
export = system
owner = nobody

[lookups]
access = read : [ admin, sc_admin, cpblty_gems_es_user ], write : [ admin, sc_admin, cpblty_gems_admin ]

####OR 

####For del_* apps: 
[]
access = read : [ admin, sc_admin, cpblty_gems_admin ], write : [ admin, sc_admin, cpblty_gems_globaloversight ]
export = system
owner = nobody

####OR (On SHC_AMER_FCMAA only)
[]
access = read : [ admin, cpblty_gems_user ], write : [ admin, sc_admin, cpblty_gems_admin, app_all_gems_metrics ]
export = system
owner = nobody


#For Indexer Applications

####For TAs 
[]
access = read : [ * ], write : [ admin, sc_admin ]
export = system
owner = nobody


####For del_* apps: 
[]
access = read : [ admin, sc_admin, cpblty_gems_admin ], write : [ admin, sc_admin, cpblty_gems_globaloversight ]
