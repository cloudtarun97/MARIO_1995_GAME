Deploying Super Mario on Kubernetes
--------------------------------------------------


Prerequisites:

--> An Ubuntu Instance

--> IAM role

--> Terraform should be installed on instance

-->  AWS CLI and KUBECTL on Instance
-----------------------------------

STEP 1: Launch Ubuntu instance

-----------------------------------

STEP 2: Create IAM role
	 	-> For permission policy select Administrator Access (Just for learning purpose), click Next.	
		-> Provide a Name for Role and click on Create role.


Go to EC2 Dashboard and select the instance.

Click on Actions --> Security --> Modify IAM role.

--> go to Rooot user Dir

-----------------------------------

STEP 3: Cluster provision

	--> git clone https://github.com/cloudtarun97/MARIO_1995_GAME.git

	--> cd k8s-mario

	--> sudo chmod +x script.sh

	--> ./script.sh

This script will install Terraform, AWS cli, Kubectl, Docker.
	
	--> docker --version
	    aws --version
	    kubectl version --client
	    terraform --version

Now change directory into the EKS-TF


NOTE: Don’t forgot to change the s3 bucket name in the backend.tf file (Create a s3 bucket name as same in the backend file)

	--> cd EKS-TF
	--> terraform init

Now run terraform validate and terraform plan

	--> terraform validate
	--> terraform plan

Now Run terraform apply to provision cluster.

--> terraform apply --auto-approve
	(Completed in 15mins)

Update the Kubernetes configuration

Make sure change your desired region

--> aws eks update-kubeconfig --name EKS_CLOUD --region ap-south-1

Now change directory back to k8s-mario

	-> cd ..
	-> ls -l 

-----------------------------------

step 4: Deployment

--> kubectl apply -f deployment.yaml

#to check the deployment 

--> kubectl get all

Now let’s apply the service


-----------------------------------

step 5: Service

--> kubectl apply -f service.yaml

#to check the deployment 

--> kubectl get all

Now let’s describe the service and copy the LoadBalancer Ingress

--> kubectl describe service mario-service


Paste the ingress link in a browser and you will see the Mario game.

-----------------------------------

Step 6: Destruction :

--> kubectl get all
--> kubectl delete service mario-service
--> kubectl delete deployment mario-deployment

--> terraform destroy --auto-approve




------------------------------------------X-----------------------------------------




