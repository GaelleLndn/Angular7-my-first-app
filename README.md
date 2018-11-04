# MyFirstApp

This project was generated with [Angular CLI](https://github.com/angular/angular-cli) version 7.0.4.

## Development server

Run `ng serve` for a dev server. Navigate to `http://localhost:4200/`. The app will automatically reload if you change any of the source files.


## COURSE:

// ***********************************************************
MISCELLEANOUS

.:: constructor = a method eecuted at the point of time the component is created by angular

.:: <ng-template #noServer>
=> <ng-template></ng-template> :  used to "mark" places in the DOM
=> #noServer : a local reference




// ***********************************************************
DIFFERENT SOLUTIONS TO CALL THE SELECTOR (Angular7 lesson:2/21)
note: 
can call by html class but NOT by html id

.:: my-component.component.ts ::.
@Component({
**  selector: 'app-my-component'   >>> html selector (prefered solution for components)
!!  selector: '[app-my-component]'  >>> html attribute
^^  selector: '.app-my-component'   >>> html class
    templateUrl: './servers.component.html',
    styleUrls: ['./servers.component.css']
})

.:: app-component.component.html::.
<div class="container">
  <div class="row>">
    <div class="col-xs-12">
        <h3>Hello</h3>
**      <app-my-component></app-my-component>   >>> html selector    
!!      <div app-my-component></div>  >>> html attribute
^^      <div class="app-my-component"></div>   >>> html class
    </div>
  </div>
</div>


// ***********************************************************
DATA BINDING (Angular7 lesson:2/22)

1) Output data

    => String Interpolation : {{ datat }}

        Can take a string, a reference to a variable or a method
        exple: 
        <p>{{ 'Server' }} with ID {{ serverId }} is {{ getServerStatus() }}</p>

    => Property Binding : [property]="data"

        .:: my-component.component.ts ::.
            export class ServersComponent implements OnInit {
                allowNewServer = false;
                constructor() {
                    setTimeout(() => { this.allowNewServer = true;}, 2000);
                }
            }

        .:: my-component.component.html ::.
            <button class="btn btn-primary" [disabled]="!allowNewServer">
                Add Server
            </button>


2) React to user Events

    => Event Binding : (event)="expression"

        .:: my-component.component.ts ::.
            serverCreationStatus = 'No Server was created';
            serverName = " "
            onServerCreated() {
                this.serverCreationStatus = 'Server created successfully';
            }
            onUpdateServerName(event : Event){
                this.serverName = (<HTMLInputElement>event.target).value
            }

        .:: my-component.component.html ::.
            <label>Serve Name</label>
            <input type="text"
                   class="form-control"
                   (input)="onUpdateServerName($event)">
            <p>{{ serverName }}</p>

            <button class="btn btn-primary"
                    [disabled]="!allowNewServer"
                    (click) = "onServerCreated()">Add Server</button>
            <p>{{ serverCreationStatus }}</p>


3) Combination of both

    => Two-Way Binding : [(ngModel)]="data"
        .:: my-component.component.ts ::.
            serverNameTwoWayBinding = 'Test Server Two Way Binding';

        .:: my-component.component.html ::.
            <label>Serve Name Two Way Binding</label>
            <input type="text"
                    class="form-control"
                    [(ngModel)]="serverNameTwoWayBinding">
            <p>{{ serverNameTwoWayBinding }}</p>



// ***********************************************************
DIRECTIVES (Angular7 lesson: 2/32)

Directives are instructions in the DOM
Usually use the "attribute" solution to call it

1) Structural Directives: they can add or remove elements of teh DOM
    Structural directives: they carry the *: 
    => *ngIf
        <p *ngIf = "serverCreated; else noServer"> Server was created</p> 
        <ng-template #noServer>
            <p>No server was created</p>
        </ng-template>
    => *ngFor
        <app-server *ngFor="let server of servers"></app-server>


2) Attribute Dircetives only change the element they are placed in
    => ngStyle
        .:: my-component.component.ts ::.
            export class ServersComponent {
                serverId: number = 10;
                serverStatus: string = 'offline'; 

                constructor() {
                    this.serverStatus = Math.random() > 0.5 ? 'online : 'offline';
                }

                getServerStatus(){
                    return this.serverStatus;
                }

                getColor(){
                    return this.serverStatus === 'online' ? 'green' : 'red';
                }
            }

        .:: my-component.component.html ::.
            <p [ngStyle]="{backgroundColor : getColor()}">{{ 'Server' }} with ID {{ serverID }} is {{ getServerStatus() }}</p>


    => ngClass
        .:: my-component.component.ts ::.
            @Component({
                selector: 'app-server',
                templateUrl: './server.component.html',
                styles: [ `
                    .online {
                    color: white;
                    }
                `]
                })
            export class ServersComponent {
                serverId: number = 10;
                serverStatus: string = 'offline'; 

                constructor() {
                    this.serverStatus = Math.random() > 0.5 ? 'online : 'offline';
                }

                getServerStatus(){
                    return this.serverStatus;
                }

                getColor(){
                    return this.serverStatus === 'online' ? 'green' : 'red';
                }
            }

        .:: my-component.component.html ::.
            <p [ngStyle]="{backgroundColor : getColor()}"
               [ngClass]="{online: serverStatus === 'online'}">
                {{ 'Server' }} with ID {{ serverId }} is {{ getServerStatus() }}
            </p>






## Code scaffolding

Run `ng generate component component-name` to generate a new component. You can also use `ng generate directive|pipe|service|class|guard|interface|enum|module`.

## Build

Run `ng build` to build the project. The build artifacts will be stored in the `dist/` directory. Use the `--prod` flag for a production build.

## Running unit tests

Run `ng test` to execute the unit tests via [Karma](https://karma-runner.github.io).

## Running end-to-end tests

Run `ng e2e` to execute the end-to-end tests via [Protractor](http://www.protractortest.org/).

## Further help

To get more help on the Angular CLI use `ng help` or go check out the [Angular CLI README](https://github.com/angular/angular-cli/blob/master/README.md).
