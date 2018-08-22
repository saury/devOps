# Jenkinsfiles

This project contains pipeline script for CI/CD of Web Front End project in Jenkins.

## Rules

For we have regular release for various project and repositorites.

Folowing steps show about how we deal with release tasks.

So, all the pipline script should refer to these steps.

### Steps:

```mermaid
graph TD;
    Title(("📓 Repositories"))
    Title-->H["🚑 Fix"]
		Title-->D["✍️ Latest commit"]

    subgraph develop
    D
    end
    subgraph release
    D-.At the end of the release day.->DRegular["🆕 Create TimeStamped <br> TAG OR BNAME"]
    end
    subgraph hot-fix?
    H-->D;
    end

    subgraph Jenkins
      subgraph Release Tasks
      D-->|"automatically"|R1["🌘 QA"]
      D-->|"manually"|R2["🌗 Staging"];
      D-->|"manually"|R3["🌕 Live"];
      end
      subgraph Pipelines
      R1-->J1
      R2-->J1
      R3-->J1
      J1["🔗 Checkout"]-->J2["🚚 Install"]
      J2-->J3["🐛 Test"]
      J3-->J4["📃 Build"]
      J4-->J5["🍺 Publish to release branch"]
      J5-->J6["☁️ Deploy to AWS S3 bucket"]
      J6-->J7["🗑 Delete Jenkins workspace"]
      end
    end
```
