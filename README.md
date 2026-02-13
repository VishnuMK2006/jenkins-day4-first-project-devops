# Jenkins Setup

This document describes:

- Jenkins installation using WAR file
- Initial Jenkins configuration
- Creating the first Jenkins project
- Building and running a Dockerized application
- Using Freestyle and Pipeline methods


## Prerequisites

- Java installed (JDK 11 or later recommended)
- Docker installed
- Node.js and npm installed
- Git installed

Verify installations:

```bash
java -version
docker -v
node -v
npm -v
git --version
````
---

# Jenkins Installation

## Step 1: Download Jenkins

Visit:

[https://www.jenkins.io/download/](https://www.jenkins.io/download/)

Download:

**Generic Java package (.war)**



## Step 2: Run Jenkins

Navigate to the download directory:

```bash
cd ~/Downloads
```

Run Jenkins:

```bash
java -jar jenkins.war
```

<img width="1920" height="785" alt="image" src="https://github.com/user-attachments/assets/b1b6ef67-c13c-4756-ad7a-0e361fe25f25" />

## Step 3: Access Jenkins

Open browser:

```
http://localhost:8080
```

<img width="1920" height="1114" alt="image" src="https://github.com/user-attachments/assets/367bf79a-9650-493a-b8c9-87a9d22265e5" />

## Step 4: Unlock Jenkins

Retrieve initial admin password:

```bash
cat ~/.jenkins/secrets/initialAdminPassword
```

Paste into Jenkins UI.


## Step 5: Install Plugins

Select:

✔ Install Suggested Plugins


## Step 6: Create Admin User

Example credentials:

```
Username: root
Password: root
```

Store credentials securely.
<img width="1920" height="1114" alt="image" src="https://github.com/user-attachments/assets/6c155b22-c890-428e-b19c-3aa8cc53a11f" />

---

# First Project Setup

## Repository Used

```
https://github.com/VishnuMK2006/jenkins-day4-first-project-devops.git
```



# Method 1: Freestyle Project

## Step 1: Create Job

1. Jenkins Dashboard → New Item
2. Enter project name
3. Select **Freestyle Project**
4. Click OK



## Step 2: Source Code Management

Select:

✔ Git

Repository URL:

```
https://github.com/VishnuMK2006/jenkins-day4-first-project-devops.git
```

Branch:

```
main
```

<img width="1920" height="1114" alt="image" src="https://github.com/user-attachments/assets/a838281b-254d-4f1c-bd81-ca5569483019" />

## Step 3: Build Steps

Add **Execute Shell**

```bash

#Add Each build as new build
echo "Installing dependencies..."  #Build 1
npm install

echo "Building project..."  #Build 2
npm run build || true

echo "Building Docker image..." #Build 3
docker build -t mywebsite:v1 .

echo "Running Docker container..." #Build 4
docker run -d -p 3000:3000 mywebsite:v1

echo "Server is running from Jenkins"  #Build 5
```
<img width="1920" height="1114" alt="image" src="https://github.com/user-attachments/assets/fbe568e7-70b8-4021-abc5-664967be6425" />

## Step 4: Save and Build

Click:

✔ Apply
✔ Save
✔ Build Now


## Output screen
<img width="1920" height="1114" alt="image" src="https://github.com/user-attachments/assets/019ea09d-9a89-4f8c-b836-975befe3721b" />

## Logs

`Started by user vishnumanikandan`
Running as SYSTEM
`Building in workspace /home/vishnumanikandan/.jenkins/workspace/git automation`
[WS-CLEANUP] Deleting project workspace...
[WS-CLEANUP] Deferred wipeout is used...
The recommended git tool is: NONE
No credentials specified
Cloning the remote Git repository
`Cloning repository` 
https://github.com/VishnuMK2006/jenkins-day4-first-project-devops.git
 > git init /home/vishnumanikandan/.jenkins/workspace/git automation # timeout=10
Fetching upstream changes from https://github.com/VishnuMK2006/jenkins-day4-first-project-devops.git
 > git --version # timeout=10
 > git --version # 'git version 2.43.0'
 > git fetch --tags --force --progress -- https://github.com/VishnuMK2006/jenkins-day4-first-project-devops.git +refs/heads/*:refs/remotes/origin/* # timeout=10
 > git config remote.origin.url https://github.com/VishnuMK2006/jenkins-day4-first-project-devops.git # timeout=10
 > git config --add remote.origin.fetch +refs/heads/*:refs/remotes/origin/* # timeout=10
Avoid second fetch
 > git rev-parse refs/remotes/origin/main^{commit} # timeout=10
Checking out Revision aea6121318a52d8cfbd82f7c5171907a1f24b4f7 (refs/remotes/origin/main)
 > git config core.sparsecheckout # timeout=10
 > git checkout -f aea6121318a52d8cfbd82f7c5171907a1f24b4f7 # timeout=10
Commit message: "Merge pull request #2 from VishnuMK2006/mian"
First time build. Skipping changelog.
[git automation] $ /bin/sh -xe /tmp/jenkins451065861153576153.sh
`+ echo 🚀 Installing dependencies...
🚀 Installing dependencies...`
+ npm install
npm WARN EBADENGINE Unsupported engine {
npm WARN EBADENGINE   package: 'react-router@7.1.5',
npm WARN EBADENGINE   required: { node: '>=20.0.0' },
npm WARN EBADENGINE   current: { node: 'v18.19.1', npm: '9.2.0' }
npm WARN EBADENGINE }
npm WARN EBADENGINE Unsupported engine {
npm WARN EBADENGINE   package: 'react-router-dom@7.1.5',
npm WARN EBADENGINE   required: { node: '>=20.0.0' },
npm WARN EBADENGINE   current: { node: 'v18.19.1', npm: '9.2.0' }
npm WARN EBADENGINE }

added 260 packages, and audited 261 packages in 3s

57 packages are looking for funding
  run `npm fund` for details

10 vulnerabilities (3 low, 6 moderate, 1 high)

To address all issues, run:
  npm audit fix

Run `npm audit` for details.
`+ echo 🏗 Building project...
🏗 Building project...`
+ npm run build

> sungo-react@0.0.0 build
> tsc -b && vite build

[36mvite v6.1.0 [32mbuilding for production...[36m[39m
transforming...
DEPRECATION WARNING [import]: Sass @import rules are deprecated and will be removed in Dart Sass 3.0.0.

More info and automated migrator: https://sass-lang.com/d/import

   ╷
17 │ @import "_mixins";
   │         ^^^^^^^^^
   ╵
    src/assets/scss/main.scss 17:9  root stylesheet

DEPRECATION WARNING [import]: Sass @import rules are deprecated and will be removed in Dart Sass 3.0.0.

More info and automated migrator: https://sass-lang.com/d/import

   ╷
19 │ @import "_variables";
   │         ^^^^^^^^^^^^
   ╵
    src/assets/scss/main.scss 19:9  root stylesheet

DEPRECATION WARNING [import]: Sass @import rules are deprecated and will be removed in Dart Sass 3.0.0.

More info and automated migrator: https://sass-lang.com/d/import

   ╷
21 │ @import "_buttons";
   │         ^^^^^^^^^^
   ╵
    src/assets/scss/main.scss 21:9  root stylesheet

DEPRECATION WARNING [import]: Sass @import rules are deprecated and will be removed in Dart Sass 3.0.0.

More info and automated migrator: https://sass-lang.com/d/import

   ╷
23 │ @import "_typography";
   │         ^^^^^^^^^^^^^
   ╵
    src/assets/scss/main.scss 23:9  root stylesheet

DEPRECATION WARNING [import]: Sass @import rules are deprecated and will be removed in Dart Sass 3.0.0.

More info and automated migrator: https://sass-lang.com/d/import

   ╷
26 │ @import "_customDropdown";
   │         ^^^^^^^^^^^^^^^^^
   ╵
    src/assets/scss/main.scss 26:9  root stylesheet

WARNING: 21 repetitive deprecation warnings omitted.
Run in verbose mode to see all warnings.

[32m✓[39m 764 modules transformed.
rendering chunks...
computing gzip size...
[2mdist/[22m[32mindex.html                                [39m[1m[2m  0.51 kB[22m[1m[22m[2m │ gzip:   0.33 kB[22m
[2mdist/[22m[2massets/[22m[32mfa-v4compatibility-C9RhG_FT.woff2  [39m[1m[2m  4.80 kB[22m[1m[22m
[2mdist/[22m[2massets/[22m[32mfa-v4compatibility-CCth-dXg.ttf    [39m[1m[2m 10.84 kB[22m[1m[22m
[2mdist/[22m[2massets/[22m[32mfa-regular-400-BjRzuEpd.woff2      [39m[1m[2m 25.47 kB[22m[1m[22m
[2mdist/[22m[2massets/[22m[32mfa-regular-400-DZaxPHgR.ttf        [39m[1m[2m 68.06 kB[22m[1m[22m
[2mdist/[22m[2massets/[22m[32mfa-brands-400-D_cYUPeE.woff2       [39m[1m[2m118.68 kB[22m[1m[22m
[2mdist/[22m[2massets/[22m[32mfa-solid-900-CTAAxXor.woff2        [39m[1m[2m158.22 kB[22m[1m[22m
[2mdist/[22m[2massets/[22m[32mfa-brands-400-D1LuMI3I.ttf         [39m[1m[2m210.79 kB[22m[1m[22m
[2mdist/[22m[2massets/[22m[32mfa-solid-900-D0aA9rwL.ttf          [39m[1m[2m426.11 kB[22m[1m[22m
[2mdist/[22m[2massets/[22m[35mindex-BqRZuACT.css                 [39m[1m[2m501.26 kB[22m[1m[22m[2m │ gzip:  80.17 kB[22m
[2mdist/[22m[2massets/[22m[36mindex-BUTOblZx.js                  [39m[1m[33m792.77 kB[39m[22m[2m │ gzip: 243.85 kB[22m
[33m
(!) Some chunks are larger than 500 kB after minification. Consider:
- Using dynamic import() to code-split the application
- Use build.rollupOptions.output.manualChunks to improve chunking: https://rollupjs.org/configuration-options/#output-manualchunks
- Adjust chunk size limit for this warning via build.chunkSizeWarningLimit.[39m
[32m✓ built in 2.95s[39m
[git automation] $ /bin/sh -xe /tmp/jenkins6770705363029805810.sh
`+ echo 🐳 Building Docker image...
🐳 Building Docker image...`
+ docker build -t mywebsite:v1 .
#0 building with "default" instance using docker driver

#1 [internal] load build definition from Dockerfile
#1 transferring dockerfile: 537B done
#1 DONE 0.0s

#2 [internal] load metadata for docker.io/library/node:20-alpine
#2 DONE 2.0s

#3 [internal] load metadata for docker.io/library/nginx:1.27-alpine
#3 DONE 2.0s

#4 [internal] load .dockerignore
#4 transferring context: 92B done
#4 DONE 0.0s

#5 [build 1/6] FROM docker.io/library/node:20-alpine@sha256:09e2b3d9726018aecf269bd35325f46bf75046a643a66d28360ec71132750ec8
#5 resolve docker.io/library/node:20-alpine@sha256:09e2b3d9726018aecf269bd35325f46bf75046a643a66d28360ec71132750ec8 0.0s done
#5 DONE 0.0s

#6 [stage-1 1/4] FROM docker.io/library/nginx:1.27-alpine@sha256:65645c7bb6a0661892a8b03b89d0743208a18dd2f3f17a54ef4b76fb8e2f2a10
#6 resolve docker.io/library/nginx:1.27-alpine@sha256:65645c7bb6a0661892a8b03b89d0743208a18dd2f3f17a54ef4b76fb8e2f2a10 0.0s done
#6 DONE 0.0s

#7 [internal] load build context
#7 transferring context: 17.23MB 0.1s done
#7 DONE 0.1s

#8 [build 2/6] WORKDIR /app
#8 CACHED

#9 [build 4/6] RUN npm install
#9 CACHED

#10 [build 5/6] COPY . .
#10 CACHED

#11 [stage-1 2/4] RUN rm /etc/nginx/conf.d/default.conf
#11 CACHED

#12 [build 3/6] COPY package*.json ./
#12 CACHED

#13 [build 6/6] RUN npm run build
#13 CACHED

#14 [stage-1 3/4] COPY --from=build /app/nginx.conf /etc/nginx/conf.d/default.conf
#14 CACHED

#15 [stage-1 4/4] COPY --from=build /app/dist /usr/share/nginx/html
#15 CACHED

#16 exporting to image
#16 exporting layers done
#16 exporting manifest sha256:7ec05a8a9d9b3a39919f1b2fc13d7f855d3fc8feb58216a87e42eed3e86a8d3b done
#16 exporting config sha256:20ee29b8042abc71aed65fa24bfae43361f085090fd032739023a36e23cb503a done
#16 exporting attestation manifest sha256:0e1cf2d4a012e2cf04bd75a9c27e93d5bb39209054c791ddb11fbd35d6ba3ff3 0.0s done
#16 exporting manifest list sha256:23eebc3ad5da26a7acc61951fd73ca7171f0b371b50aa128f457e2a99bd27e99 done
#16 naming to docker.io/library/mywebsite:v1 done
#16 unpacking to docker.io/library/mywebsite:v1 0.0s done
#16 DONE 0.1s
[git automation] $ /bin/sh -xe /tmp/jenkins13552382043254450619.sh
`+ echo Server is running from jenkins
Server is running from jenkins`
`+ docker run -d -p 3000:3000 mywebsite:v1`
ad6a9c6418879f530f0d6e0508495c86ca6053dabd7dde08918e8239012389a2
`Finished: SUCCESS`



---

# Method 2: Freestyle Project with Triggers
## Step 1: Enable Build Trigger

In job configuration:

✔ Build periodically

Use cron expression generated from:

[https://crontab.guru/](https://crontab.guru/)

Example:

```
H/5 * * * *
```

(Runs every 5 minutes)


## Step 2: Save Job

✔ Save

Jenkins will trigger builds automatically.

---

# Method 3: Pipeline Project

## Step 1: Create Pipeline Job

1. Jenkins Dashboard → New Item
2. Enter name
3. Select **Pipeline**
4. Click OK


## Step 2: Pipeline Script

```groovy
pipeline {
    agent any

    environment {
        IMAGE_NAME = "mywebsite"
        TAG = "v1"
    }

    stages {

        stage('Checkout Code') {
            steps {
                git branch: 'main',
                    url: 'https://github.com/VishnuMK2006/jenkins-day4-first-project-devops.git'
            }
        }

        stage('Build App') {
            steps {
                sh 'npm install'
                sh 'npm run build || true'
            }
        }

        stage('Build Docker Image') {
            steps {
                sh 'docker build -t $IMAGE_NAME:$TAG .'
            }
        }

        stage('Run Container') {
            steps {
                sh '''
                docker stop mycontainer || true
                docker rm mycontainer || true
                docker run -d -p 3000:3000 --name mycontainer $IMAGE_NAME:$TAG
                '''
            }
        }
    }
}
```

<img width="1920" height="1114" alt="image" src="https://github.com/user-attachments/assets/45362ee8-19d5-498d-8946-bd099c74d599" />

## Step 3: Save and Run

✔ Save
✔ Build Now

## Pipeline

<img width="1920" height="1114" alt="image" src="https://github.com/user-attachments/assets/4b38471d-234b-4c20-95da-3a8ca20f59ab" />

# Verification

Check running containers:

```bash
docker ps
```

Access application:

```
http://localhost:3000
```
# Final Output Screen

<img width="1920" height="1114" alt="image" src="https://github.com/user-attachments/assets/019ea09d-9a89-4f8c-b836-975befe3721b" />
