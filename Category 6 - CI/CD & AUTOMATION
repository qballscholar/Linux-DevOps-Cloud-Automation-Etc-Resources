**\========================================**  
**CATEGORY 6: CI/CD & AUTOMATION**  
**\========================================**

**6.1 JENKINS FUNDAMENTALS:**

**/\* COMMENT: Jenkins is the leading open-source automation server for CI/CD pipelines.**  
   **Understanding Jenkins architecture, job types, and pipeline syntax is essential for**  
   **modern DevOps practices. \*/**

**KEY CONCEPTS:**  
**• Master-Agent Architecture: Distributed build system**  
**• Freestyle Jobs: Basic job configuration**  
**• Pipeline as Code: Declarative and Scripted pipelines**  
**• Jenkins Plugins: Extend functionality**  
**• Build Triggers: Webhooks, polling, scheduled builds**

**JENKINS PIPELINE EXAMPLE:**  
**pipeline {**  
    **agent any**  
    **stages {**  
        **stage('Build') {**  
            **steps {**  
                **sh 'mvn clean package'**  
            **}**  
        **}**  
        **stage('Test') {**  
            **steps {**  
                **sh 'mvn test'**  
            **}**  
        **}**  
        **stage('Deploy') {**  
            **steps {**  
                **sh './deploy.sh'**  
            **}**  
        **}**  
    **}**  
**}**

**BEST PRACTICES:**  
**• Use Pipeline as Code (Jenkinsfile in source control)**  
**• Implement proper secret management**  
**• Use agents/slaves for distributed builds**  
**• Implement build caching for faster execution**  
**• Set up proper backup and disaster recovery**

**6.2 GITLAB CI/CD:**

**/\* COMMENT: GitLab provides integrated CI/CD directly in the repository platform.**  
   **The .gitlab-ci.yml file defines the entire pipeline, making it version-controlled**  
   **and easy to manage alongside code. \*/**

**KEY CONCEPTS:**  
**• .gitlab-ci.yml: Pipeline configuration file**  
**• Runners: Agents that execute jobs**  
**• Stages: Sequential phases (build, test, deploy)**  
**• Jobs: Individual tasks within stages**  
**• Artifacts: Files passed between jobs**

**GITLAB CI EXAMPLE:**  
**stages:**  
  **\- build**  
  **\- test**  
  **\- deploy**

**build-job:**  
  **stage: build**  
  **script:**  
    **\- echo "Building application"**  
    **\- npm install**  
    **\- npm run build**  
  **artifacts:**  
    **paths:**  
      **\- dist/**

**test-job:**  
  **stage: test**  
  **script:**  
    **\- npm test**

**deploy-job:**  
  **stage: deploy**  
  **script:**  
    **\- ./deploy.sh**  
  **only:**  
    **\- main**

**BEST PRACTICES:**  
**• Use cache to speed up builds**  
**• Implement proper environment-specific deployments**  
**• Use Docker for consistent build environments**  
**• Implement manual approval for production deploys**

**6.3 GITHUB ACTIONS:**

**/\* COMMENT: GitHub Actions enables automation directly within GitHub repositories.**  
   **Workflows are defined in YAML and can trigger on various GitHub events,**  
   **making it perfect for CI/CD and automation tasks. \*/**

**KEY CONCEPTS:**  
**• Workflows: Automated processes in .github/workflows/**  
**• Events: Triggers like push, pull\_request, schedule**  
**• Jobs: Set of steps running on the same runner**  
**• Steps: Individual tasks (actions or commands)**  
**• Marketplace: Reusable actions from community**

**GITHUB ACTIONS EXAMPLE:**  
**name: CI/CD Pipeline**

**on:**  
  **push:**  
    **branches: \[ main \]**  
  **pull\_request:**  
    **branches: \[ main \]**

**jobs:**  
  **build:**  
    **runs-on: ubuntu-latest**  
    **steps:**  
    **\- uses: actions/checkout@v3**  
    **\- name: Setup Node.js**  
      **uses: actions/setup-node@v3**  
      **with:**  
        **node-version: '18'**  
    **\- name: Install dependencies**  
      **run: npm install**  
    **\- name: Run tests**  
      **run: npm test**  
    **\- name: Build**  
      **run: npm run build**

**BEST PRACTICES:**  
**• Use GitHub-hosted runners for simplicity**  
**• Leverage marketplace actions to avoid reinventing wheels**  
**• Store secrets in GitHub Secrets**  
**• Use matrix builds for multiple environments**  
**• Implement status checks for pull requests**

**6.4 ANSIBLE AUTOMATION:**

**/\* COMMENT: Ansible is agentless automation using SSH and YAML playbooks.**  
   **Perfect for configuration management, application deployment, and orchestration.**  
   **No agents needed makes it simpler to manage than alternatives. \*/**

**KEY CONCEPTS:**  
**• Playbooks: YAML files defining automation tasks**  
**• Inventory: List of managed hosts**  
**• Modules: Reusable units of work**  
**• Roles: Organized, reusable playbook components**  
**• Idempotent: Safe to run multiple times**

**ANSIBLE PLAYBOOK EXAMPLE:**  
**\---**  
**\- name: Configure web servers**  
  **hosts: webservers**  
  **become: yes**  
  **tasks:**  
    **\- name: Install nginx**  
      **apt:**  
        **name: nginx**  
        **state: present**  
        **update\_cache: yes**  
      
    **\- name: Start nginx service**  
      **service:**  
        **name: nginx**  
        **state: started**  
        **enabled: yes**  
      
    **\- name: Deploy website**  
      **copy:**  
        **src: /local/website/**  
        **dest: /var/www/html/**  
        **mode: '0644'**

**INVENTORY EXAMPLE:**  
**\[webservers\]**  
**web1.example.com**  
**web2.example.com**

**\[databases\]**  
**db1.example.com**

**COMMON COMMANDS:**  
**ansible-playbook playbook.yml \-i inventory**  
**ansible all \-m ping \-i inventory**  
**ansible-galaxy install geerlingguy.nginx**  
**ansible-vault encrypt secrets.yml**

**BEST PRACTICES:**  
**• Use roles to organize complex playbooks**  
**• Implement vault for sensitive data**  
**• Use tags for selective execution**  
**• Test with \--check mode before applying**  
**• Keep playbooks idempotent**
