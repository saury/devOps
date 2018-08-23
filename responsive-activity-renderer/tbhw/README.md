# Workflow

```mermaid
graph TD;
    subgraph branches
    subgraph develop
        C[new commit]
    end
    subgraph release
        RB[new bundle]
        C-.At the end of the release day.->DRegular["🆕 Create TimeStamped <br> TAG OR BNAME"]
    end
    end
    subgraph jenkins
        C --> |auto|B["DailyBuild"]
        B --> |success|RB
        B --> |success|DQ

        subgraph Deploy
            DQ["QA"]
            DS["Staging"]
            DL["Live"]
            RB -.- DQ
            RB -.- DS
            RB -.- DL
        end
    end
```
