##Background

When you want to get data out of an OpenMRS system, it is sometimes worthwhile to have programmers or advanced administrators design a very specific report or data export, such as might be run "monthly, for each clinic." But sometimes mid-level want to be able to do "ad hoc" analyses and exports, where they explore data and export it on the fly.

The Reporting Module provides powerful and flexible tools for Row-Per-(Patient, Visit, Encounter, etc) exports, however this functionality only has an administrative UI that is unsuitable for an end user.

The Reporting Compatibility Module has two key tools (Cohort Builder and Data Export) with friendlier UIs (though they are quite dated). Though these are used by many implementations, they are built on top of a deprecated query and export framework, and they are really past what should be the end of their useful lifetime.
Objectives

The goal of this project is to build a tool that can be used by doctors and data analysts to do Ad Hoc queries and exports of data. These queries may happen in response to an on-the-fly question from a hospital manager, or in response to a specific suspicion or need that a clinician has to analyze certain data. We want to allow people to access the necessary data without needing a developer or advanced sysadmin to be a bottleneck in the process.

Specifically, we want to build a UI around row-per-domain-object exports for key domain objects (primarily Patient, Visit, Encounter, and Obs) that is suitable for users of medium sophistication.

We want to design the tool in a way that it can be used to query for domain objects matching certain criteria (like the Cohort Builder), and also to export details of the matching objects (like the Data Export tool).
##Design

The Reporting Module has a RowPerObjectDataSetDefinition base class (with implemantations for Patient, Encounter, etc), and under the hood we should be building instances of this.

The Reporting Module also supports the idea of "definition libraries" (see the AllDefinitionLibraries class) which include built-in and implementation-configured queries and data definitions. Rather than trying to give users full access to all of the primitive queries in the reporting module, we will focus on letting them access definitions encapsulated in these libraries.
##Status

Considerable initial work has been done on this tool already, in the reportingui module, but there is much left to do. 

Further work is captured under the following JIRA epics:

    RA-261 (version 1): https://issues.openmrs.org/browse/RA-261
    RA-279 (version 2): https://issues.openmrs.org/browse/RA-279

##Dev Notes

The code is at https://github.com/openmrs/openmrs-module-reportingui. See all files and packages that have "adhoc" in the name.

The easiest way to test out this code is to:

    check out code from https://github.com/openmrs/openmrs-distro-referenceapplication
    add the latest snapshot version of the reportingui module to pom.xml (in several places, alongside everywhere you find the "reporting" module)
    follow the instructions at Developer How-To Launch a Local Instance of the Reference Application
    The entry point to the tool should be at http://localhost:8080/openmrs/reportingui/adHocManage.page
        alternately you can enable the "reportingui_adHocAnalysis" feature toggle, to see a link in the UI.
