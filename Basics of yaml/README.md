# Basics of YAML

## Step-01: Comments & Key Value Pairs
- Space after colon is mandatory to differentiate key and value
```yml
# Defining simple key value pairs
name: rizwan
age: 25
city: Pune
```

## Step-02: Dictionary / Map
- Set of properties grouped together after an item
- Equal amount of blank space required for all the items under a dictionary
```yml
person:
  name: rizwan
  age: 25
  city: Pune
```

## Step-03: Array / Lists
- Dash indicates an element of an array
```yml
person: # Dictionary
  name: rizwan
  age: 25
  city: pune
  hobbies: # List  
    - riding
    - swimming
  hobbies: [riding, swimming]   # List with a differnt notation  
```  

## Step-04: Multiple Lists
- Dash indicates an element of an array
```yml
person: # Dictionary
  name: rizwan
  age: 25
  city: pune
  hobbies: # List  
    - riding
    - swimming
  hobbies: [riding, swimming]   # List with a differnt notation  
  friends: # 
    - name: friend1
      age: 22
    - name: friend2
      age: 25            
```  


## Step-05: Sample Pod Tempalte for Reference
```yml
apiVersion: v1 # String
kind: Pod  # String
metadata: # Dictionary
  name: demo-app
  labels: # Dictionary 
    app: myapp         
spec:
  containers: # List
    - name: demo-app
      image: nginx
      ports:
        - containerPort: 80
          protocol: "TCP"
        - containerPort: 81
          protocol: "TCP"
```



