this contains yaml files for secrets and config maps. in configmpas we have used env variables for username and later secret to encode the password , we have also used config files for mongo "  mongodb.conf: |
    storage:
      dbPath: /data/db
    replication:
        replSetName: "rs0"   "


---------


for that teh statefulset.yaml ../statefulset  we have added a in command field --config=/etc/mongo/mongodb.conf , where this file has to be read while starting the pod, in our case we had to create this file on our container using ---------volumes:
        - name: mongodb-config
          configMap:
            name: mongodb-config
            items:
              - key: mongodb.conf
                path: mongodb.conf



------- The key read from configmap(mongodb.conf) and then saved to file mongodb.conf.this later while mounting we use volumeMount ------name: mongodb-config         mountPath: /etc/mongo--------



the to check we can login into the pods using "kubectl exec -it podname -- sh"  check for env variables and then look for the /etc/mongo/mongodb.config.   this is the magic :P
 
