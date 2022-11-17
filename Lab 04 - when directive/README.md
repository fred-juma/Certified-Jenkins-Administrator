### When directive

#### The *when* directive specifies conditions that must be met for Pipeline to execute the *stage*. It must contain at least one condition; it supports nested conditions.

#### In this lab we create and edit a simple pipeline to demonstrate usage of when directive

#### Lab Objectives
+ Specifies that the "Confirm Deploy to Staging" and "Deploy to Staging" steps run only when building from the **when-directive-test** branch.


When Directive Stage View               |  
:-------------------------:|
![Pipleline Visualization](https://github.com/fred-juma/Certified-Jenkins-Administrator/blob/main/images/Lab04_when_directive_stage_view.JPG)



#### Commonly used Built-in when conditions

+ **branch** - Execute the stage when the branch being built matches the branch pattern given. For example, this code specifies that this stage should only run on the master branch:

```bash
when {
  branch 'master'
}
```

+ **environment** - execute the *stage* when the specified environment variable is set to the given value:

```bash
when {
  environment name: 'DEPLOY_TO', value: 'production'
}
```

+ **expression** - execute the *stage* when the specified expression evaluates to true:

```bash
when {
  expression {
    return params.DEBUG_BUILD
  }
}
}
```

+ **equals** - compares two values and returns true if they’re equal. You can also do "not equals" comparisons using the not { equals … } syntax.

```bash
pipeline {
    agent any
    stages {
        stage('Build') {
            steps {
                sh 'make package'
            }
        }
        stage('Test') {
            when { equals expected: 2, actual: currentBuild.number }
            steps {
                sh 'make check'
            }
        }
        stage('Deploy') {
            steps {
                echo 'Deploying only because this commit is tagged...'
                sh 'make deploy'
            }
        }
    }
}

```

+ **changeRequest** - returns true if this Pipeline is building a change request, such as a GitHub or Bitbucket pull request:

```bash
`when { changeRequest authorEmail: "joe@example.com" }`
```

+ **beforeAgent** - Allows you to specify that the *when* conditions should be evaluated before entering the agent for the stage. When *beforeAgent true* is specified, you do not have access to the agent’s workspace, but you can avoid unnecessary SCM checkouts and waiting for a valid agent to be available:

```bash
pipeline {
    agent none
    stages {
        stage('Example Build') {
            steps {
                echo 'Hello World'
            }
        }
        stage('Example Deploy') {
            agent {
                label "some-label"
            }
            when {
                beforeAgent true
                branch 'production'
            }
            steps {
                echo 'Deploying'
            }
        }
    }
}
```
+ **not** - Executes the stage when the nested condition is false.

```bash
when { not { branch 'master' } }
```

+ **allOf** - Execute the stage when all nested conditions are true:

```bash
when {
  allOf {
    branch 'master'
    environment name: 'DEPLOY_TO', value: 'production' // AND
  }
}
```


+ **anyOf** - execute the stage when at least one of the nested conditions is true

```bash
when {
  anyOf {
    branch 'master'
    branch 'staging' // OR
  }
}
```