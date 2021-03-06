# Darwin
Darwin is an open source Artificial Intelligence Framework for CyberSecurity.  
Using AI-powered algorithms, it can detect suspicious behaviours and threats in your environnment.  
Its high availability and modularity, coupled with the capabilities of Vulture, allows it to analyze a wide range 
of data sources and raise alerts on your environnments.  
For more information on Darwin capabilities and documentation, you can have a look __<a href="https://github.com/VultureProject/darwin" target="_blank">here</a>__!  

# Inputs and Outputs
Internally, Darwin is a manager handling a list of independent programs running a specific algorithm, those programs are called "**filters**".  
Each filter waits for specific entry(ies), depending on its needs (see __<a href="https://github.com/VultureProject/darwin/wiki" target="_blank">the documentation</a>__ for more details), and generates a score from this data.  
The score generated by each filter can be **any number between 0 and 100** (included). This score is then compared to a threshold given to the filter: if the score is under the threshold nothing is generated, if the **score is above or equal to the threshold an alert is generated and log is potentially enriched**.  

## Alerts
When the score obtained by a specific entry(ies) is above or equal to the configured threshold, filters will generate an **alert containing the details and the data** triggering the alert. Alerts can be seen in the **[Logviewer](/darwin/logviewer/)** or can be forwarded using a Listener with mode *LOG*, listening mode *FILE*, and filepath */var/log/darwin/reconciled_alerts.log*.

## Enrichment
With alerts, **Darwin can also be configured to "enrich" log lines**. When assigning Darwin Policies to a Listener, this Listener's output can be **enriched with tags** when alerts are generated. This enrichment allows to mark log lines presenting suspicious data (such as DGA).  
Enrichment can be activated for every type of Listener, but **will only have a meaningful impact on LOG Listeners**.

# Darwin Security policies
This menu lists all your configured policies when using Darwin.  
As Darwin is very modular, you can use it for very different purposes. Policies are a way to define __use-cases__ of detection in Vulture 
that you will be able to assign to data sources afterward.  
Darwin policies allow you to __classify__ and __concentrate__ algorithms on specific tasks to tackle your detection needs easily!

## Name
The friendly name of your policy.

## Description
A potential description for your policy.

## Inputs
The list of inputs (data sources) assigned to this policy.  
Darwin takes profit of the diversity and availability of sources on Vulture: you can execute algorithms on passive network sniffing, internal firewall logs, WAF flux, and logs sent and parsed locally.  
All the __[Listeners](/services/frontend/)__ in Vulture can be used as data sources for Darwin.  
An input can be assigned to policy(ies) with 2 different modes:
- **generate alerts** will simply send entries to filters, without waiting for answers. Only alerts will be generated by Darwin. This is faster.
- **enrich logs and generate alert** will send entries and wait for a score. Alerts will be generated by Darwin, but logs will also be enriched. This is slower. 

## Status
The status of each filter in the policy.  
Statuses have 3 states :
- ![status_green](/static/img/status_green.png) The filter is enabled and running
- ![status_grey](/static/img/status_grey.png) The filter is not enabled, is not installed, or Darwin is down
- ![status_red](/static/img/status_red.png) The filter is enabled, but is not running properly

# Edit/Clone/Delete
## Editing
By clicking on the line corresponding to a policy,, you can edit its configuration.  
This includes:
- Its name
- Its description
- The filters in it
- The parameters of each filter

## Cloning
The copy button is a shortcut to creating a new policy with the same parameters as the cloned policy, this can be useful to try a variant of an existing policy or create several policies with similar filters.

## Deleting
This button allows to delete an existing policy.  
Be careful, __a policy cannot be removed if assigned to input(s)__