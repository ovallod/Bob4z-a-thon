# Lab: Bob Premium for Z Skill - COBOL Generation and Validation

## Objective

This lab demonstrates the use of the **Bob Premium for Z** skill to generate COBOL programs compliant with IBM Enterprise COBOL for z/OS with CICS standards, then automatically validate the syntax with **Z Open Editor**. In Z Open Editor, you can open the generated file and validate the syntax directly in the editor. You have the option to modify the syntax rules by configuring the zCodeScan rules (https://www.ibm.com/docs/en/developer-for-zos/17.0.x?topic=overview-linting-zcodescan).

## Prerequisites

- VS Code with Z Open Editor installed
- CBSA workspace open

## Defining Coding Standards

Before generating the Skill, we will define the COBOL coding standards from existing code.

### Bob Prompt
```text
Define COBOL coding standards by analyzing existing COBOL programs.
```
### Result
COBOL coding standards defined in **docs/GLOBAL-docu-standards-cobol.md**.

Standards derived from analysis of programs BNKMENU, BNK1CAC, CREACC, ABNDPROC and BANKDATA
Formalized rules on program structure, naming, copybooks, CICS/SQL management, abends, validations and data access



## Creating the Skill
We will use the skill builder to create a Bob Premium for Z skill that will generate a COBOL program and validate it according to coding standards and validate its syntax with Z Open Editor.


### Bob Prompt

```text
Create a Bob Premium for Z skill, using the skill builder, that allows to:
- generate a COBOL program that respects the coding standards defined in docs/GLOBAL-docu-standards-cobol.md
- then verify using Z Open Editor, the syntax and standard of the generated COBOL. Syntax errors must be corrected by Bob.
```
### Result

Bob will use the `coding-standards-skill-builder` skill to create the `cobol-generator-validator` skill in `.bob/skills/` with:
- `skill.yaml`: skill configuration
- `skill.py`: generation and validation logic
- `templates/`: COBOL code templates
- `requirements.txt`: dependencies


## Activating the Skill

The skill activates automatically with these phrases:
- "Generate a COBOL program"
- "Create a COBOL"
- "Validate COBOL"
- "Bob Premium for Z"

## Example 1: Simple Program Generation

### Request

```
Generate a COBOL program that allows finding a customer's account from their phone number
```

### Expected Result

Bob will:

1. **Analyze the requirements for the phone search program**
2. **Check the CUSTOMER copybook structure for the phone field**
3. **Generate the COBOL program compliant with IBM standards**
4. **Validate with Z Open Editor**
5. **Correct detected errors**



## Example 2: CICS Program with BMS Map

### Request

```
Create a COBOL program with Bob Premium for Z that uses a BMS map 
to display and update bank account information.
The program should be called UPDTACCT and use a pseudo-conversational pattern.
```

### Expected Result

Bob generates a complete program with:
- Pseudo-conversational pattern (COMMAREA)
- BMS map management (SEND/RECEIVE)
- User input validation
- MAPFAIL error handling
- DISPLAY-MODE and UPDATE-MODE structure

## Applied Standards

### 1. Compilation Directives

**CICS Standard:**
```cobol
PROCESS CICS,NODYNAM,NSYMBOL(NATIONAL),TRUNC(STD)
CBL CICS('SP,EDF')
```

**CICS + DB2:**
```cobol
PROCESS CICS,NODYNAM,NSYMBOL(NATIONAL),TRUNC(STD)
CBL CICS('SP,EDF')
CBL SQL
```

**CICS + DLI:**
```cobol
PROCESS CICS,NODYNAM,NSYMBOL(NATIONAL),TRUNC(STD)
CBL CICS('SP,EDF,DLI')
```

### 2. Naming Conventions

| Element | Convention | Example |
|---------|-----------|---------|
| WS Variables | `WS-` + descriptive | `WS-CUSTOMER-ID` |
| Paragraphs | Verb + object | `PROCESS-CUSTOMER-RECORD` |
| Condition names | Descriptive state | `VALID-CUSTOMER` |
| Constants | Uppercase + hyphens | `MAX-RECORDS` |

### 3. CICS Error Handling

**Mandatory Pattern:**
```cobol
EXEC CICS [COMMAND]
    [PARAMETERS]
    RESP(WS-CICS-RESP)
    RESP2(WS-CICS-RESP2)
END-EXEC.

IF WS-CICS-RESP NOT = DFHRESP(NORMAL)
    MOVE '[OPERATION]' TO WS-ERROR-OPERATION
    PERFORM HANDLE-CICS-ERROR
END-IF.
```



## Conclusion

The **Bob Premium for Z** skill completely automates the process of generating and validating COBOL programs compliant with IBM Enterprise COBOL for z/OS with CICS standards.

**Key Benefits:**
- ✅ Automatic generation compliant with standards
- ✅ Validation with Z Open Editor
- ✅ Automatic error correction
- ✅ Complete documentation
- ✅ Production-ready code

**To get started:**
Simply say "Generate a COBOL program with Bob Premium for Z" and follow the instructions!

---

**Version**: 1.0.0  
**Date**: 2026-05-12  
**Author**: Bob for Z Team
