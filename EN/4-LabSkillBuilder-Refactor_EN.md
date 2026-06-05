# Advanced Bob Premium for Z Exercises
## Exercise 1: Coding Standard Skill | Exercise 2: VSAM to DB2 Refactoring

**Estimated duration:** 1-2 hours  
**Level:** Advanced  
**Prerequisites:** Knowledge of COBOL and CICS

---

## 📋 Table of Contents

1. [Exercise 1: Generating a Custom Coding Standard Skill](#exercise-1-generating-a-custom-coding-standard-skill)
2. [Exercise 2: VSAM to DB2 Refactoring](#exercise-2-vsam-to-db2-refactoring)

---

## Exercise 1: Generating a Custom Coding Standard Skill

### 🎯 Objective

Create a custom coding standard skill that analyzes your existing COBOL code and automatically generates reusable documented standards to ensure code consistency across the entire team.

### 🔧 Bob Mode to Use

**Mode: 🧰 Z Code**

---

## 📋 Step-by-Step Scenario

### **Step 1: Initial Skill Generation**

#### 💬 Bob Prompt

```
Generate a coding standard skill in my workspace by analyzing the existing COBOL programs
```

#### ⚙️ What Bob Does

Bob will:
1. Analyze all COBOL programs in the workspace
2. Identify recurring coding patterns (naming, structures, error handling)
3. Generate three files in `.bob/`:
   - `CBSA-standards-reference.md`: Standards documentation
   - `CBSA-example.md`: Examples of compliant code
   - `skills.md`: Skill definition

#### ✅ Expected Result

Bob creates three files documenting:
- Naming conventions (programs, variables, paragraphs)
- Standard program structure
- Error handling (codes 0-9)
- CICS and SQL patterns
- Code quality rules

---

### **Step 2: Standard Customization (Optional)**

#### 💬 Bob Prompt

```
Modify the file CBSA-standards-reference.md to add the following rules:
- Counter variables must start with CTR-
- Validation paragraphs must end with -VALIDATION
- Add a section on logging standards
```

#### ⚙️ What Bob Does

Bob updates the reference file with your specific rules and integrates the new conventions into the skill.

---

### **Step 3: Code Generation with the Standard**

#### 💬 Bob Prompt

```
Create a COBOL program for me that:
- Searches for a customer by email
- Validates the email format
- Returns the customer information if found
- Handles all possible errors

Follow CBSA-standards-reference.md for the structure and conventions
```

#### ⚙️ What Bob Does

Bob will:
1. Read the file `CBSA-standards-reference.md`
2. Apply all documented standards
3. Generate a complete and compliant COBOL program (e.g. `BNKINQE.cbl`)
4. Document the code with appropriate comments

---

## 💡 Added Value

| Aspect | Without Skill | With Skill |
|--------|---------------|------------|
| Standards analysis | 2-3 days | 2 minutes |
| Documentation | Incomplete | Comprehensive |
| Code generation | Variable standards | Guaranteed standards |
| Consistency | Variable | 100% |
| Onboarding | 2-3 weeks | 1-2 days |

**Overall gain: 95% reduction in time**

---

## 📋 Use Cases

1. **Onboarding**: Clear standards reference for new developers
2. **Modernization**: Generate new code consistent with legacy code
3. **Harmonization**: Unified standards across the organization
4. **Audit**: Documented and traceable standards

---

## 🎓 Key Takeaways

### ✅ Benefits

- **Automation**: Bob automatically extracts patterns
- **Reusability**: The skill applies to all your future developments
- **Consistency**: Guarantees code uniformity
- **Scalable**: The skill can be updated over time

### ⚠️ Points of Attention

1. Verify the detected standards during the first generation
2. Adapt the generated files to your specific needs
3. Update the skill when your standards evolve
4. Share the skill with the whole team

---

## Exercise 2: VSAM to DB2 Refactoring

### 🎯 Objective

Modernize an existing COBOL program that uses VSAM files by refactoring it to use DB2, while maintaining functional compatibility and improving performance.

### 🔧 Bob Mode to Use

**Mode: 📐 Z Architect**

---

## 📋 Step-by-Step Scenario

### **Step 0: Create the extractionGoal.md Document**

#### 💬 Bob Prompt

```
Create a document extractionGoal.md that defines the refactoring principles for migrating from VSAM to DB2, including:

1. Functionality Preservation
2. Mapping VSAM Operations to SQL
3. Transaction Management
4. Sequential Access Optimization
5. Robust Error Handling
6. Use of Host Variables
7. Performance Optimization
8. Structure and Modularity
9. Compatibility and Progressive Migration
10. Documentation and Traceability

Also include a refactoring checklist and success criteria.
```

#### ⚙️ What Bob Does

Bob creates the file `extractionGoal.md` (485 lines) containing:
- 10 detailed principles with COBOL examples
- VSAM→DB2 mapping tables
- A 3-phase checklist
- Measurable success criteria

---

### **Step 1: Analyze the Existing VSAM Program**

#### 💬 Bob Prompt

```
Analyze the BNKCUST program that uses VSAM files and identify:
- The VSAM operations used (READ, WRITE, REWRITE, DELETE, STARTBR, READNEXT)
- The data structures being manipulated
- The access keys and indexes
- The data access patterns
- The complexity points for migration
```

#### ⚙️ What Bob Does

Bob will:
1. Analyze the COBOL code to identify all CICS VSAM commands
2. Extract the data structures (copybooks, working-storage)
3. Identify the primary and secondary keys used
4. Document the access patterns
5. Assess migration complexity for each operation

#### ✅ Expected Result

Bob generates a detailed analysis report with:
- VSAM files used (type, keys, length)
- Identified operations (READ, STARTBR/READNEXT, REWRITE, WRITE, DELETE)
- Migration complexity table
- Recommendations (create DB2 table, replace operations, add indexes)

---

### **Step 2: Design the DB2 Data Model**

#### 💬 Bob Prompt

```
Propose a DB2 data model to replace the CUSTOMER VSAM file, including:
- The table DDL definition
- The necessary indexes
- Integrity constraints
- Performance considerations
```

#### ⚙️ What Bob Does

Bob will:
1. Analyze the existing VSAM structure
2. Design the optimal DB2 schema
3. Generate the DDL scripts (CREATE TABLE, INDEX, CONSTRAINTS)
4. Propose the appropriate indexes
5. Document the design choices

#### ✅ Expected Result

Bob generates:
- Complete DDL scripts for the CUSTOMER table
- Indexes on primary and secondary keys
- CHECK and DEFAULT constraints
- Documentation of design decisions

---

### **Step 3: Interactive Refactoring with the Skill Command**

#### 💬 Bob Prompt (Mode 🧰 Z Code)

```
/refactor BNKCUST.cbl extractionGoal.md
```

**Explanation**:
- `/refactor`: Interactive refactoring skill command
- `BNKCUST.cbl`: Source file to refactor
- `extractionGoal.md`: Document containing the principles

#### ⚙️ What Bob Does

Bob launches the **interactive refactoring workflow** in 4 phases:

**Phase 1 - Analysis**:
- Detects all VSAM operations
- Loads the principles from extractionGoal.md
- Proposes a refactoring plan

**Phase 2 - Validation**:
- Presents each VSAM→SQL transformation
- Requests user confirmation

**Phase 3 - Generation**:
- Generates the refactored code progressively
- Replaces READ with SELECT, STARTBR/READNEXT with CURSOR, etc.
- Adds transaction management (COMMIT/ROLLBACK)

**Phase 4 - Final Report**:
- Generates a BEFORE/AFTER comparison report
- Documents all changes

#### ✅ Expected Result

Refactored COBOL program with:
- All VSAM operations replaced by SQL
- DB2 cursors for sequential access
- Complete transaction management
- Robust SQL error handling
- COMMAREA compatibility preserved

---

### **Step 4: Migration Plan and Testing**

#### 💬 Bob Prompt

```
Create a complete migration plan to move from VSAM to DB2, including:
- The migration steps
- The testing strategy
- The rollback plan
- Performance considerations
- The validation checklist
```

#### ⚙️ What Bob Does

Bob generates a detailed migration plan in 5 phases:

1. **Preparation**: Create DB2 environment, migrate data
2. **Development**: Refactor code, unit tests
3. **Integration Testing**: Functional, performance, and load testing
4. **Deployment**: Cutover, post-deployment validation
5. **Stabilization**: Monitoring, optimization

Also includes:
- Rollback plan (2 scenarios)
- Risk and mitigation matrix
- Final validation checklist

---

## 💡 Added Value

| Aspect | Manual Approach | With Bob |
|--------|-----------------|----------|
| VSAM analysis | 2-3 days | 10 minutes |
| DB2 design | 3-5 days | 15 minutes |
| Code refactoring | 1-2 weeks | 30 minutes |
| Migration plan | 3-5 days | 20 minutes |

**Overall gain: 90-95% reduction in time**

---

## 📋 Use Cases

1. **Progressive Modernization**: Step-by-step migration of VSAM files
2. **Performance Improvement**: Faster complex queries with DB2
3. **Modern Integration**: Data access from web/mobile applications
4. **Compliance and Audit**: Guaranteed referential integrity

---

## 🎓 Key Takeaways

### ✅ Migration Benefits

- **Performance**: DB2 optimized for complex queries
- **Integrity**: ACID constraints and transactions
- **Flexibility**: Standard SQL, joins, aggregations
- **Integration**: Easier access from other systems

### ⚠️ Points of Attention

1. Test under real production load before go-live
2. Maintain the existing COMMAREA interface
3. Properly manage COMMIT/ROLLBACK
4. Monitor DB2 after migration
5. Train the team on SQL and DB2

### 💡 Best Practices

- **Comprehensive testing**: Validate all scenarios
- **Progressive migration**: One program at a time
- **Continuous monitoring**: Track DB2 performance
- **Rollback ready**: Tested fallback plan

---

## 🚀 Summary of Key Prompts

### Exercise 1 - Coding Standards

```
1. Generate a coding standard skill in my workspace by analyzing the existing COBOL programs

2. Modify the file CBSA-standards-reference.md to add the following rules: [...]

3. Create a COBOL program for me that [...] Follow CBSA-standards-reference.md
```

### Exercise 2 - VSAM→DB2 Refactoring

```
1. Create a document extractionGoal.md that defines the refactoring principles [...]

2. Analyze the BNKCUST program that uses VSAM files and identify: [...]

3. Propose a DB2 data model to replace the CUSTOMER VSAM file [...]

4. /refactor BNKCUST.cbl extractionGoal.md

5. Create a complete migration plan to move from VSAM to DB2 [...]
```

---

## 📊 Measurable Gains

| Exercise | Task | Without Bob | With Bob | Gain |
|----------|------|-------------|----------|------|
| **1** | Coding Standards | 2-3 days | 2 minutes | 99.9% |
| **2** | VSAM→DB2 Migration | 3-4 weeks | 75 minutes | 99.5% |

---

**Version:** 1.0  
**Date:** June 2, 2026  
**Author:** Bob Premium for Z Team

**Transform the way you work with the mainframe! 🚀**