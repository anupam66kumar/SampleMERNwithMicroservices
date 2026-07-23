# **`MERN Microservices Application with CI/CD & Kubernetes Deployment`** 

```
A full-stack MERN microservices application containerized with Docker, automated
via Jenkins CI, stored in AWS ECR, deployed onto an Amazon EKS cluster, and
integrated with MongoDB Atlas.
```

### **`GitHub Repo: https://github.com/anupam66kumar/SampleMERNwithMicroservices.git`** 

```
---
```

```
Architecture Overview
* **Frontend:** React.js served via Nginx (Port 80)
* **Backend Services:** Node.js microservices (`helloservice` on port 3001,
`profileservice` on port 3002)
* **Database:** MongoDB Atlas (Cloud-hosted database cluster)
* **CI/CD Pipeline:** Jenkins declarative pipeline script (`Jenkinsfile`)
* **Orchestration:** Kubernetes (Amazon EKS) managed via `kubectl` and custom
manifests
```

```
---
```

```
## Project Directory Structure
```

```
SampleMERNwithMicroservices/
├── backend/
│   ├── helloservice/
│   │   ├── Dockerfile
│   │   ├── index.js
│   │   └── package.json
│   └── profileservice/
│       ├── Dockerfile
│       ├── index.js
│       └── package.json
├── frontend/
│   ├── Dockerfile
│   ├── package.json
│   └── src/
├── k8s/
│   └── all-services.yaml
└── Jenkinsfile
```

# **Step-by-Step Implementation** 

## **1. CI/CD Pipeline Automation (Jenkins & ECR)** 

The application uses a `Jenkinsfile` at the root directory to automate checking out code, logging into AWS ECR, building images, and pushing them securely. 

- **Jenkins Pipeline Execution:** _(screenshot of successful Jenkins build ):_ 



<!-- Start of picture text -->
€ > CG ff — 8s jenkinsacademics.herovired.com/job/AnupamStreaminApp-Pipeline/<br>Er © herovired ( SAACert © StocksPicks [) Knowledge © mediumart © citrix % Bookmarks @ RainyMood-R... 4g Techt<br>*) Jenkins = AnupamStreaminApp-Pipe...<br>&) status ~ AnupamStreaminApp-Pipeline<br></> Changes<br>CP Buildi  Now Stage9  View<br>{6} Configure . ;<br>Declarative: Build and Push<br>W Delete Pipelinemes. C h ockseckout SCM Checkout Code Services:<br><> Move Average stage times: 910ms 654ms 2min 48s<br>(full run time: ~2min 51s) © " a<br>Q Full Stage View ©<br>.<br>sy Favorite 4123FY commit1 910ms 654ms 2min 48s<br>@ Open Blue Ocean<br>© Stages Permalinks<br>a Rename ij -<br>e Last build (#3), 1 hr 43 min ago<br>@® Pipeline—  syntax Last stable build (#3)(#3), 1 hr43 min ago<br>« Last successful build (#3), 1 hr 43 min ago<br>« Last completed build (#3), 1 hr 43 min ago<br>Builds > ose<br>Q Filter /<br>Today<br>© #3 5:34AM v<br><!-- End of picture text -->



<!-- Start of picture text -->
€ > CG A © 82 jenkinsacademics.herovired.com/job/AnupamStreaminApp-Pipeline/3/stages/ * O48 ©:<br>88 Cherovired (© SAACert © StocksPicks [4 Knowledge © mediumart © citrix + Bookmarks @ RainyMood-R... 4¥ TechBenchby... @ Ep. 184- Robe... Free AlTools:... @ FreeAl Writing... »<br>re Jenkins | AnupamStreaminApp-Pipe... v #3 VY — Stages Q oO = ©<br>Q #3 @ Reun vB<br>@ Started byherovired © Started1hr45minago §% Queued3ms © Took2min51seconbuilt-in + </> Changes<br>Start End<br>g g @<br>Checkout SCM Checkout Code Build and Push<br>Services +<br>Q Search > ¥) Build and Push Services © 2m48s © Startedih45mago (J Jenkins ooo<br> Checkoutscm 0.885 J awsecr get-login-password ~region ap-southeast-2| docker login -usernameAWS ~password-stdin 951066974787.dkr.ecr.ap-southeast-2.amazon... > s G<br>v Checkout Code 0.625<br>v Checksif running ona Unix-likenode > 35ms<br>v) Build and Push:Servites 2m 48s<br>v docker build -t "$JD_IMAGE" ./backend/helloService > Bs G<br>v Checksif running on a Unix-likenode > 47ms  @<br>v) docker tag "$JD_ID" "$JD_TAGGED_IMAGE_NAME" > 028 GF<br>YD Checksif running ona Unix-like node > 25ms<br>¥) docker push "$JD_TAGGED_IMAGE_NAME” > 1s G<br>Y Checksif running ona Unix-like node > 3ams_<br>v docker build -t "$JD_IMAGE" ./backend/profileService > 3<br>~~ > stn tht= iss fhe<br><!-- End of picture text -->



<!-- Start of picture text -->
| € CG @ 8% ap-southeast-2.console.aws.amazon.com/ecr/private-registry/repositories?region=ap-southeast-2 * SO4£6 6:<br>EE © herovired [ SAACert (© StocksPicks [ Knowledge © mediumart © citrix % Bookmarks @ Rainy Mood-R & TechBench by. i) Ep. 184- Robe. @ Free Al Tools: @ Free Al writing »<br>“5 | GO La AEC B) | S| @ | & | Asterecitetsycne) y  paministratorAccess/AnupamKumarSingh<br>(=) Amazon ECR > Private registry > Repositories ira<br>Amazon Elastic < Private repositories (3) () t mane x ’ (create repository<br>Container Registry Q Search by repository substring<br>¥ Private registry<br>Repositories Repository name a | ur | Created at v_ | Tag immutability | Encryption type |<br>Features& Settings IE) 951066974787.dkr.ecr.ap-so aaa<br>¥ Public registry frontend utheast-2.amazonaws.com/frontea (uTc+05.5)edie 7 Mutable AES-256<br>Repositories [[) 951066974787.dkr.ecr.ap-so hineaibeoeieoseee<br>Settings helloservice utheast-2.amazonaws.com/helloservice (UTC+05.5)spd Mutable AES-256<br>ECR public gallery 12 I) 951066974787.dkr.ecr.ap-so Maver oronloceena<br>Amazon ECS 7 profileservice utheast-2.amazonaws.com/profileservice (UTC+05.5)sbirmes : Mutable AES-256<br>Amazon EKS 17<br>Getting started 2<br>Documentation 7<br><!-- End of picture text -->

|:<br>§ kubectl get nodes|||||
|---|---|---|---|---|
|NAME<br>1909_168<br>4149<br>c<br><“t_3¢<br>1<br>ip-192-168-55-112.ap-southeast-2.compute.internal|STATUS<br>Ready|ROLES<br>S<br>5<br><none>|AGE<br>4<br>10m|VERS<br>vwi.3|
|4.9-eks-8f14419<br>=<br>9<br>=<br>=<br>7<br>¢-<br>|<br>ip-192-168-64-46.ap-southeast-2.compute. internal<br>4.9-eks-8f14419|Ready|2<br>=<br><none>|4<br>10m|=<br>= wi.3|



|S$ kubectl get pods|||||
|---|---|---|---|---|
|NAME|READY|STATUS|RESTARTS|AGE|
|frontend-depLoyment -5645b6697d-6qwzw|1/1|Running|0|55m|
|heLloservice-depLloyment -7f5cf4cc98 -9wkzb|1/1|Running|0|55m|
|profileservice-depLoyment-7cd87bfc68-x/7vvz|1/1|Running|)|46m|



S$ curl http://localhost:3001/ 



<!-- Start of picture text -->
+ GC A © localhost:aoas Be Ss 8! @ :<br>B83  COherovired (© SAACert (© StocksPicks [4 Knowledge © mediumart © citrix % Bookmarks @ Rainy Mood-R &g TechBench by i) Ep. 184 - Robe @ Free Al Tools: @ Free Al writing »<br>Welcome<br>Profile<br><!-- End of picture text -->



<!-- Start of picture text -->
ne CG A  ANbotsecure a1bs6df7928494ffca91a36f8daa7004-1721128661 .ap-southeast-2.elb.amazonaws.com * O4+F 8B @©:<br>BS Oherovired (© SAACert (© StocksPicks [4 Knowledge © mediumart © citrix % Bookmarks @ RainyMood-R... 4 TechBenchby @ Ep. 184 - Robe OQ Free Al Tools: @ Free Al writing »<br>Welcome<br>Profile<br><!-- End of picture text -->

