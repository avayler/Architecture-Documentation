# Glossary & Ubiquitous Language

## SaaS Platform

| Term | Brief / Long Winded Description |
|------|---------------------------------|
| FOE  | Fuilfilment Orchestration Engine |
| MF   | Mobile Fitment (namespace for code translated from TOD / TOTD and into newer serverless format) |
| RBAC | Role Based Access Control |
| CPE  | Customer Portal Engine |

## Workstreams & Apps

| Term                                      | Brief / Long Winded Description |
|-------------------------------------------|---------------------------------|
| SP & DR                                   | Slot Processing and Dynamic Routing. |
| TechApp (aka Colleague App or Fitter App) | The app on a handset of the tyre fitters out in the vans. Used to organise and record their jobs on a given day |
| WeCheck (aka MCheck or BikeCheck)         | In store apps to replace Halfords paper checks regarding the state of repair of cars and bikes                  |

## Dynamic Routing

| Term                  | Brief / Long Winded Description |
|-----------------------|---------------------------------|
| Time Slot             | A period of time that promises to fulfil the provided set of service(s) that will expire after an elapsed period of time. This can then be used to reserve or confirm that period of time on a schedule |
| Reserve / Reservation | Reserving a period of time on a schedule |
| Confirm               | Confirm a period of time on a schedule |
| Manifest              | A logical container for set period of time at a service location stating which of its resources have actions to carry out, and in what sequence |
| Descartes             | A third party company that provides scheduling optimisation services for mobile fittings |
| Schedule              | A logical phase for a period of time that contains resources and bookings |
| Planning Schedule     | A schedule where adjustments can be made and new bookings added and availability for new bookings requested |
| Review Schedule       | A schedule where only manual adjustments can be made, availability can no longer be requested |
| Execution Schedule    | A schedule where only manual adjustments can be made and is what is planned to occur |
| Draft Manifest        | A manifest that is only current at the time of the request |
| Final Manifest        | A manifest that can be assumed to be the final version and what is planned to occur |
| Booking Reference     | A reference that is used to refer to a unique instance for a single service action, can refer to a set of services that can be carried out at the same time.  Commonly a fulfilment / order  / basket. Should be used during all scheduling Availability Requests, Reservation and Confirmation requests and during the FOE Booking Process |
| OMS                   | Order management system |
| Route                 | An ordered list of stops that include 1 Start stop (Type = 0) 1 End stop (Type = 1) and, at least 1 Job stop (Type = 3) between Start and End |

## Time Slot Processing

| Term                        | Brief / Long Winded Description |
|-----------------------------|---------------------------------|
| Action                      | The Action represents an abstract modification over the TimeSlot. An Actions may be added to a Processing Step to be applied to the TimeSlot sequentially or may be applied to the TimeSlot independently. At this moment the system provides the following predefined Actions: ApplayDefaultValuesAction, MarkAsGreenVanAction, MarkAsOperationalAction, and SetupThePriceAction |
| Apply Default Values Action | Modifies the following properties of the TimeSlot: Price, IsGreenVan, IsOperational if they are provided |
| Condition                   | The condition contains an instance of MF.SDK.Engine and may be attached to Processing Step. Condition will affect the direction that will be followed by the TimeSlot inside the Flow |
| Flow                        | The Flow is a part of the TimeSlot Processing Engine that may contain Processing Steps chained each to other. Each Flow has the following attributes: StartDate, EndDate, IsActiveByDefault, and Priority. These attributes will be used by the TimeSlot Processing Engine to choose the Flow that will be passed by the provided TimeSlot |
| Mark As Green Van Action    | Marks the TimeSlot as GreenVan / Environmentally Friendly |
| Mark As Operational Action  | Marks the TimeSlot as Operational |
| Processing Step             | The Processing Steps are main building bricks that may be used to build a Flow. Each Processing Step may contain a Condition, list of Actions, After Actions Step and Instead of Actions Step |
| Setup The Price Action      | Setups the Price for the TimeSlot to the provided value |
| Time Slot                   | The TimeSlot it is an object that is valuable for business. TimeSlot Processing Engine process over TimeSlots to enrich them with the following attributes: Price, IsGreenVan, and IsOperational |
| Time Slot Processing Engine | The TimeSlot Processing Engine is a system that provides an ability to build a Flows. After TimeSlot comes to the system it may pass through one of defined Flows. |

## Tech App

| Term            | Brief / Long Winded Description |
|-----------------|---------------------------------|
| Big Blue Box    | The collection of data enrichment services which gather information from Scheduling / FOE and Sub-components of the Tech-App module which results in the final form of data which will be provided to the mobile-handset application                                                                                    |                                                                                    
| IElement        | The generic data model within the Tech-App module which is the vehicle for the majority of data associated with the Survery Admin UX applications and the Mobile handset application and their associated back-end systems                                                                                              |                                                                                   
| Survey Template | A set of data expressed in the format of a  ‘tree / branch data structure’ using the ‘IElement’ data model  to express the relationship between a survey, it’s pages, their sections and their questions which is defined by the consumer in the Survey Admin UX Application and is subject to change at any time       |       
| Survey Instance | The ‘immutable published version’ of a survey template, it is the instance that is rendered to the mobile handset application and is specific for that IElement of type:survey (EG: StartOfDay) / type:job (Tyre Fitting Job) / type:job_item (Tyre Product),  or type:break (ancillary tasks between jobs and surveys) | 

## Halfords Terminology

| Term | Brief / Long Winded Description |
|------|---------------------------------|
| HME  | Halfords Mobile Expert - Halfords brand naming for TyresOnTheDrive |
| HAC  | Halfords Auto Centres |

## General

| Term | Brief / Long Winded Description |
|------|---------------------------------|
| DSR  | Digital Service Record |
| VRH  | Vehicle Repair History |

## Service Delivery

| Term | Brief / Long Winded Description |
|------|---------------------------------|
| MTTR | Mean time to respond - SLA for response time to accept or reject a service defect or degredation occurance |
| MTTF | Mean time to fix - SLA describing time widow from response to fix delivery |
