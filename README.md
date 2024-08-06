# Angular-Python

1. create a button in angular to open a new window where I'll have 4 text box for user input

To create a button in Angular that opens a new window with four text boxes for user input, you'll need to follow these steps:

1. **Set up the Angular project**: Make sure you have an Angular project set up. If not, you can create one using the Angular CLI.

2. **Create a component for the new window**: This component will contain the four text boxes.

3. **Create the button to open the new window**: This button will be in your main component.

Here's a step-by-step guide:

### Step 1: Set Up the Angular Project

If you haven't already set up an Angular project, you can do so with the Angular CLI:

```bash
ng new my-angular-app
cd my-angular-app
ng serve
```

### Step 2: Create a Component for the New Window

Create a new component called `UserInputComponent`:

```bash
ng generate component user-input
```

### Step 3: Implement the UserInputComponent

Edit `user-input.component.html` to include four text boxes:

```html
<div>
  <h2>User Input Form</h2>
  <form>
    <label for="input1">Input 1:</label>
    <input type="text" id="input1" name="input1" /><br /><br />

    <label for="input2">Input 2:</label>
    <input type="text" id="input2" name="input2" /><br /><br />

    <label for="input3">Input 3:</label>
    <input type="text" id="input3" name="input3" /><br /><br />

    <label for="input4">Input 4:</label>
    <input type="text" id="input4" name="input4" /><br /><br />

    <input type="submit" value="Submit" />
  </form>
</div>
```

### Step 4: Implement the Button to Open the New Window

In your main component (e.g., `app.component.ts`), create a method to open the new window:

```typescript
import { Component } from "@angular/core";

@Component({
  selector: "app-root",
  templateUrl: "./app.component.html",
  styleUrls: ["./app.component.css"],
})
export class AppComponent {
  title = "my-angular-app";

  openNewWindow() {
    window.open("user-input", "_blank", "width=600,height=400");
  }
}
```

Edit `app.component.html` to include the button:

```html
<button (click)="openNewWindow()">Open Input Form</button>
```

### Step 5: Configure Routing

To ensure that the new component can be accessed via a new window, configure your routing in `app-routing.module.ts`:

```typescript
import { NgModule } from "@angular/core";
import { RouterModule, Routes } from "@angular/router";
import { UserInputComponent } from "./user-input/user-input.component";

const routes: Routes = [
  { path: "user-input", component: UserInputComponent },
  { path: "", redirectTo: "/home", pathMatch: "full" },
];

@NgModule({
  imports: [RouterModule.forRoot(routes)],
  exports: [RouterModule],
})
export class AppRoutingModule {}
```

### Step 6: Run Your Application

Make sure everything is set up correctly and run your application:

```bash
ng serve
```

Now, when you click the button, it should open a new window with the `UserInputComponent` containing the four text boxes.

By following these steps, you should have a functioning button in Angular that opens a new window with four text boxes for user input.

2. Now collect the information typed in these text boxes in variable

To collect the information typed in the text boxes into variables, you'll need to use Angular's two-way data binding with `ngModel` and create a form to handle the input data. Here’s how you can do it:

### Step 1: Enable FormsModule

First, ensure that `FormsModule` is imported in your `AppModule` so you can use `ngModel`.

Edit `app.module.ts` to include `FormsModule`:

```typescript
import { NgModule } from "@angular/core";
import { BrowserModule } from "@angular/platform-browser";
import { FormsModule } from "@angular/forms"; // Import FormsModule

import { AppComponent } from "./app.component";
import { UserInputComponent } from "./user-input/user-input.component";
import { AppRoutingModule } from "./app-routing.module";

@NgModule({
  declarations: [AppComponent, UserInputComponent],
  imports: [
    BrowserModule,
    FormsModule, // Add FormsModule here
    AppRoutingModule,
  ],
  providers: [],
  bootstrap: [AppComponent],
})
export class AppModule {}
```

### Step 2: Update the UserInputComponent

Edit `user-input.component.ts` to define the variables and a method to handle the form submission:

```typescript
import { Component } from "@angular/core";

@Component({
  selector: "app-user-input",
  templateUrl: "./user-input.component.html",
  styleUrls: ["./user-input.component.css"],
})
export class UserInputComponent {
  input1: string = "";
  input2: string = "";
  input3: string = "";
  input4: string = "";

  onSubmit() {
    console.log("Input 1:", this.input1);
    console.log("Input 2:", this.input2);
    console.log("Input 3:", this.input3);
    console.log("Input 4:", this.input4);
  }
}
```

Update `user-input.component.html` to use `ngModel` for two-way data binding and handle the form submission:

```html
<div>
  <h2>User Input Form</h2>
  <form (ngSubmit)="onSubmit()">
    <label for="input1">Input 1:</label>
    <input
      type="text"
      id="input1"
      name="input1"
      [(ngModel)]="input1"
    /><br /><br />

    <label for="input2">Input 2:</label>
    <input
      type="text"
      id="input2"
      name="input2"
      [(ngModel)]="input2"
    /><br /><br />

    <label for="input3">Input 3:</label>
    <input
      type="text"
      id="input3"
      name="input3"
      [(ngModel)]="input3"
    /><br /><br />

    <label for="input4">Input 4:</label>
    <input
      type="text"
      id="input4"
      name="input4"
      [(ngModel)]="input4"
    /><br /><br />

    <input type="submit" value="Submit" />
  </form>
</div>
```

### Step 3: Implement the Button to Open the New Window

In your main component (e.g., `app.component.ts`), ensure the method to open the new window is properly implemented:

```typescript
import { Component } from "@angular/core";

@Component({
  selector: "app-root",
  templateUrl: "./app.component.html",
  styleUrls: ["./app.component.css"],
})
export class AppComponent {
  title = "my-angular-app";

  openNewWindow() {
    window.open("user-input", "_blank", "width=600,height=400");
  }
}
```

Edit `app.component.html` to include the button:

```html
<button (click)="openNewWindow()">Open Input Form</button>
```

### Step 4: Configure Routing

Ensure your routing is properly configured in `app-routing.module.ts`:

```typescript
import { NgModule } from "@angular/core";
import { RouterModule, Routes } from "@angular/router";
import { UserInputComponent } from "./user-input/user-input.component";

const routes: Routes = [
  { path: "user-input", component: UserInputComponent },
  { path: "", redirectTo: "/home", pathMatch: "full" },
];

@NgModule({
  imports: [RouterModule.forRoot(routes)],
  exports: [RouterModule],
})
export class AppRoutingModule {}
```

### Step 5: Run Your Application

Make sure everything is set up correctly and run your application:

```bash
ng serve
```

When you click the button, it will open a new window with the `UserInputComponent` containing the four text boxes. The user inputs will be collected in the component variables and logged to the console upon form submission.

3. Now I have a docker/Kubernetes pod running in the background. I want to send this collected data to the pod and execute a python file in the pod. Tell me how to connect this Angular code with pod and how to send the data. What changes do I have to make in configuration files in angular and pod

To send the collected data from your Angular application to a Docker/Kubernetes pod and execute a Python file in the pod, you need to follow these steps:

1. **Create a backend service**: This service will receive the data from the Angular frontend and forward it to the Kubernetes pod.
2. **Expose the backend service**: Ensure that the backend service is accessible from the Angular frontend.
3. **Modify the Angular application**: Update the Angular code to send the collected data to the backend service.
4. **Handle the data in the backend service**: Forward the data to the pod and execute the Python script.
5. **Configure Kubernetes**: Ensure the pod and services are properly configured and exposed.

### Step 1: Create a Backend Service

We'll create a simple Express.js server that can receive the data from the Angular frontend and send it to the Kubernetes pod.

#### Install Node.js and Express

First, install Node.js and create a new directory for the backend service:

```bash
mkdir backend-service
cd backend-service
npm init -y
npm install express body-parser axios
```

#### Create `server.js`

Create a `server.js` file in the `backend-service` directory:

```javascript
const express = require("express");
const bodyParser = require("body-parser");
const axios = require("axios");

const app = express();
app.use(bodyParser.json());

app.post("/send-data", async (req, res) => {
  const { input1, input2, input3, input4 } = req.body;

  // Send data to the Kubernetes pod
  try {
    const response = await axios.post("http://your-pod-service/send-data", {
      input1,
      input2,
      input3,
      input4,
    });
    res.status(200).send(response.data);
  } catch (error) {
    console.error(error);
    res.status(500).send("Error sending data to pod");
  }
});

const PORT = process.env.PORT || 3000;
app.listen(PORT, () => {
  console.log(`Server is running on port ${PORT}`);
});
```

### Step 2: Expose the Backend Service

Create a `Dockerfile` for the backend service:

```dockerfile
FROM node:14

WORKDIR /app

COPY package*.json ./
RUN npm install

COPY . .

EXPOSE 3000

CMD ["node", "server.js"]
```

Build and run the Docker image:

```bash
docker build -t backend-service .
docker run -p 3000:3000 backend-service
```

### Step 3: Modify the Angular Application

Update your Angular service to send data to the backend service:

#### Create a service in Angular

```bash
ng generate service data
```

#### Edit `data.service.ts`

```typescript
import { Injectable } from "@angular/core";
import { HttpClient } from "@angular/common/http";
import { Observable } from "rxjs";

@Injectable({
  providedIn: "root",
})
export class DataService {
  private backendUrl = "http://localhost:3000/send-data"; // Backend service URL

  constructor(private http: HttpClient) {}

  sendData(data: any): Observable<any> {
    return this.http.post(this.backendUrl, data);
  }
}
```

#### Update `user-input.component.ts`

```typescript
import { Component } from "@angular/core";
import { DataService } from "../data.service";

@Component({
  selector: "app-user-input",
  templateUrl: "./user-input.component.html",
  styleUrls: ["./user-input.component.css"],
})
export class UserInputComponent {
  input1: string = "";
  input2: string = "";
  input3: string = "";
  input4: string = "";

  constructor(private dataService: DataService) {}

  onSubmit() {
    const data = {
      input1: this.input1,
      input2: this.input2,
      input3: this.input3,
      input4: this.input4,
    };
    this.dataService.sendData(data).subscribe(
      (response) => {
        console.log("Response from backend:", response);
      },
      (error) => {
        console.error("Error sending data to backend:", error);
      }
    );
  }
}
```

### Step 4: Handle the Data in the Backend Service

Create an endpoint in your pod to receive the data and execute the Python script. Assume you have a Flask server running in your pod.

#### Create a Flask server in the pod

```python
from flask import Flask, request, jsonify
import subprocess

app = Flask(__name__)

@app.route('/send-data', methods=['POST'])
def receive_data():
    data = request.json
    input1 = data.get('input1')
    input2 = data.get('input2')
    input3 = data.get('input3')
    input4 = data.get('input4')

    # Execute Python script with the received data
    result = subprocess.run(['python', 'script.py', input1, input2, input3, input4], capture_output=True, text=True)

    return jsonify({'output': result.stdout})

if __name__ == '__main__':
    app.run(host='0.0.0.0', port=5000)
```

#### Create a `Dockerfile` for the Flask server

```dockerfile
FROM python:3.8-slim

WORKDIR /app

COPY requirements.txt requirements.txt
RUN pip install -r requirements.txt

COPY . .

EXPOSE 5000

CMD ["python", "app.py"]
```

#### Build and push the Docker image

```bash
docker build -t flask-service .
docker tag flask-service:latest your-docker-repo/flask-service:latest
docker push your-docker-repo/flask-service:latest
```

### Step 5: Configure Kubernetes

Create a `Deployment` and `Service` for the Flask server in Kubernetes.

#### `deployment.yaml`

```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: flask-service
spec:
  replicas: 1
  selector:
    matchLabels:
      app: flask-service
  template:
    metadata:
      labels:
        app: flask-service
    spec:
      containers:
        - name: flask-service
          image: your-docker-repo/flask-service:latest
          ports:
            - containerPort: 5000
```

#### `service.yaml`

```yaml
apiVersion: v1
kind: Service
metadata:
  name: flask-service
spec:
  selector:
    app: flask-service
  ports:
    - protocol: TCP
      port: 80
      targetPort: 5000
  type: LoadBalancer
```

Apply the configurations:

```bash
kubectl apply -f deployment.yaml
kubectl apply -f service.yaml
```

### Summary

- **Backend service**: Created using Express.js to receive data from Angular and send it to the Kubernetes pod.
- **Angular application**: Updated to send collected data to the backend service.
- **Flask server in pod**: Receives data from the backend service and executes a Python script.
- **Kubernetes configuration**: Set up Deployment and Service for the Flask server.

By following these steps, you can connect your Angular application to a Kubernetes pod and send the collected data to execute a Python file in the pod.
