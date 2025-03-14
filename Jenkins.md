				**Jenkins Interview Questions:**

## Q1. What is CI/CD Pipeline ?
**A:** A CI/CD pipeline is an automated workflow used to build, test and deploy softwares. It ensures that code changes are integrated, verified and deployed without human intervention. 

## Q2:
**A:**

## Q3. What are the steps involved in Jenkins Pipeline ?
**A:** Jenkins pipelines automates the application build,Quality checks, tests and Deployment process.
- Jenkins pipelines are two types. 
  1. Declarative
  2. Scripted
--- Steps Names: Code Checkout, Build, Quality Gates, Unit tests, Deployment.

## Q4. Describe about SCM ?
**A:**

## Q5. How many Pipelines you built ?
**A:** 

## Q6. Different types of Pipeline ?
**A:** Declarative and Scripted.

## Q7. What are Build Quality Gates ?
**A:** Build Quality gates are pre-defined checks or conditions, that a software build must pass before progessing to the next step.
## Key Aspects of Build Quality gates:
- Automation testing
- Code Quality Checks
- Vulnerabilites checks
- Perfomance Benchmarks.
- Eg: SonarQube will be used as Build Quality gate in Jenkins.   

## Q9. How to Achieve the skipping the QA Person ?
**A:** We can skip the QA approval's or tests by using the not condition in the check steps.
```bash
pipeline {
    agent any
    parameters {
        booleanParam(name: 'SKIP_QA', defaultValue: false, description: 'Skip QA Testing')
    }
    stages {
      stage('QA Approval') {
            **when {
                expression { return !params.SKIP_QA }  // Skip if SKIP_QA is true
            }**
            steps {
                input message: "QA Approval Needed. Proceed?"
            }
        }
  }
}
```

## Q10. 
## Questions & Answers

</details>
<summary>In general, what do you need in order to communicate?</summary><br><b>

  - A common language (for the two ends to understand)
  - A way to address who you want to communicate with
  - A Connection (so the content of the communication can reach the recipients)

</b>
</details>
