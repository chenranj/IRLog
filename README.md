# CAG Service Request Change Log

> **Attributes that @Gregory added:**
>
> - `Claims_Adjuster_Generalist`
> - `Claims_Adjuster_Generalist_Supervisor`

## Claims mail WF

### Added CAG attribute for 25 steps except:

- All the Script, Call, Go To, Case, End steps
- Dispatch PRAC NE
- Imported Estimates
- Med Audit PRAC NE
- Med Audit PG

### Changed the code in Routing: 

Search `MARK: 04-15-2022` in the file for all changes:

```vbscript
' Added Claims Adjuester Generalist attribute to Assign_To
strClaims = Task.GetAttributeObject("Claims_Adjuster_Generalist").Value
strClaimsSupervisor	 = Task.GetAttributeObject("Claims_Adjuster_Generalist_Supervisor").Value
...
' Added Claims Adjuster Generalist attribute to Assign_TO group.
case "Claims Adjuster Generalist"
	checkUser = strClaims
	checkSupervisor = strClaimsSupervisor
	fallbackAdjuster = strPrimary
	fallbackSupervisor = strPrimarySupervisor
```

### Added attributes in properties of Routing

<p style="color:green"><b>Double checked all step nodes that there's no step related assignment group left.</b></p>

## Email Receiver WF

### Added attributes in properties of Email Routing

### Changed the code in email Routing

Search `MARK: 04-15-2022` in the file for all changes:

```vbscript
' Added Claims Adjuester Generalist attribute to Assign_To
strClaims = Task.GetAttributeObject("Claims_Adjuster_Generalist").Value
strClaimsSupervisor	 = Task.GetAttributeObject("Claims_Adjuster_Generalist_Supervisor").Value
...
' MARK: 04-15-2022 - Added new attribute 
claimsT = createTask(strClaims, strClaimsSupervisor)
```

<p style="color:green"><b>Double checked all step nodes that there's no step related assignment group left.</b></p>

## Query WF

### Added attributes in properties of Get Adjusters Query

### Changed the code in Get Adjuster Query

Search `MARK: 04-15-2022` in the file for all changes:

```vbscript
' MARK: 04-15-2022 - Added Claims Adjuster Generalist attribute.
Task.GetAttributeObject("Claims_Adjuster_Generalist").Value = "NOT FOUND"	Task.GetAttributeObject("Claims_Adjuster_Generalist_Supervisor").Value = "NOT FOUND"
...
Case objRecordSet("Role_CODE").Value = "clm_adj_gen"
Task.GetAttributeObject("Claims_Adjuster_Generalist").Value = objRecordSet("ADJUSTER_LOGIN_NAME").Value
Task.GetAttributeObject("Claims_Adjuster_Generalist_Supervisor").Value = objRecordSet("SUPERVISOR_LOGIN_NAME").Value
```

<p style="color:green"><b>Double checked all step nodes that there's no step related assignment group left.</b></p>
