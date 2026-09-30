
[Architecture Overview](../../Architecture%20Overview.md) > [Processes](../Processes.md)

# Scheduling Processes

Scheduling Process

## 1 Coverage Check

The aim is to determine the nearest service location which can provide the service category to the customer E.g. “Tyre Fitting”. Coverage requires knowledge of the location of the customer, this should be supplied by the customer and can be any location the customer wants to resolve the coverage from. For static service delivery (delivery at a garage workshop) the location can be approximate as we are looking for nearest locations for the customer to make the journey to. N.B. For mobile service delivery where the service is done at a location convenient to the customer (their home or work locations) then the data requirement here would be for an accurate geo-located address to drive the routing calculations as the routing calculations will derive available time-slots and therefore rule out non-routable addresses on given days, coverage may still be calculated using approximate locations like [Postcode out-code](https://en.wikipedia.org/wiki/Postcodes_in_the_United_Kingdom#:~:text=The%20outward%20code%20is%20the,mail%20is%20to%20be%20sent.) or standard Zip.

## 2 Service Constraints Determination

This activities goal is to obtain a set of constraints to be used within the availability calculation. What we are looking for are high level indicators for requirements to deliver the service. This may be thinks like job specific bays, vehicle specific needs and delivery timings. Some of this information can be obtained from an IA (industry Enabler) and other data points may be specific for a given customers implementation. We do not at present have a good mechanism to surface customer specific deviations for job constraints from the information provided by an IA. The data points discovered here are a data requirement of the “Availability Calculation” process to find appropriate asset resource(s) to calculate Time-Slots against. This step may require data relating to the identification of a vehicle to enable the IA to find specific constraints appropriate to the job on a particular vehicle. Examples of these constraints outside of servicing times are:

- MOT
- 10-Tonne Lift
- Level 3 Technician

## 3.1 Availability Calculation

This is the heart of the scheduling process in which we are tasked with calculating the delivery Time-Slots to offer as “Customer promises”. An extreme simplistic view of this task is to find the appropriate Assets which can deliver the Service Job at the selected Location and calculate Time-Slots results from the available space on those Asset Diaries, reduced to a set of unique Time-Slots across a requested period of day(s).

## 3.2 Availability Reservation

The process of placing a longer soft-hold on a specific Time-Slot reservation than is created during the calculation process. the distinction between the time all time-Slots are reserved in a calculation result vs the length a Time-Slot is held for a Singular reservation is to prevent requests fro locking other users out of obtaining jobs for long periods. The reasoning is if a single slot is selected then the desire to confirm it is stronger then the results of all slots.

## 3.3 Booking Confirmation

The action which takes a Reserved Time-Slot and places a confirmed diary entry against a Service Location Asset. These are the actual bookings against the asset(s) and will have the non-customer facing delivery times, however it is required to maintain a record of the Time-Slot which was actually booked which will allow for diary optimisation while maintaining agreed customer promises.

## 4 Booking Approval

This is an optional part of the process. It is unclear whether this is a current requirement but it is included here for completeness as it has been a requirement of customers using an affiliate / franchise model. This step takes the confirmed bookings and allows a Service Location owner, booking manager to approve or reject jobs. If a job is rejected there is an exceptions process to be followed to notify and liaise with the customer to find a suitable replacement booking if possible, if this process is in play then it should be clear to the customer that the result of 3.3 is not a firm guarantee that the customer promise will be met and that the job may still be rejected by their chosen delivery location. The job should still be locatable within the Avayler system in an un-scheduled state, the ability to move the job to another service location and re-schedule would be required.

## What is a Time-Slot?

Time-Slots are an expression of a Promise made to a Customer to deliver the requested services on a given day inside a specified time-frame. An example Time-Slot would be to express a start time to commence a Job within a two hour window, for example a two hour window 10:00 to 12:00, this does not mean any work is guaranteed to be completed within that two hour slot, just that work would commence within that two hour period. This allows for Jobs to be moved to other Assets so a Service locations daily Job load can be optimised (moved earlier, later or to other appropriate assets) and still meet agreed customer promises.
