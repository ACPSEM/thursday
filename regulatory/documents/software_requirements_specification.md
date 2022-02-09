---
id: SRS-001
revision: 1
title: Software Requirements Specification
---

# Purpose

This document describe *what* {{ device.name }} software must do.

This document is meant to be read and agreed-upon by the project owners and by software developers during design and construction.

{% if not device.samd %}
The document also provides traceability between system requirements and software requirements.
{% endif %}

[[FDA-CPSSCMD:srs]]

# Scope

This document applies to {{ device.name }} release {{ device.version }}.

# Definitions

The **Food and Drug Administration (FDA)** is a United State government agency responsible for protecting the public health by ensuring the safety, efficacy, and security of human and veterinary drugs, biological products, and medical devices.

The **Health Insurance Portability and Accountability Act** (HIPAA) is a United States law designed to provide privacy standards to protect patients' medical records and other health information provided to health plans, doctors, hospitals and other healthcare providers.

**Protected Health Information** (PHI) means individually identifiable information that is created by {{ device.name }} and relates to the past, present, or future physical or mental health or condition of any individual, the provision of health care to an individual, or the past, present, or future payment for the provision of health care to an individual.

A **User** is a person who interacts with (i.e., operates or handles) the device.

**UI** is an acronym for user interface.

# Users

Users of this device will be the various operators of a departments Treatment Planning System (TPS) in which they will execute the scripts via the built-in scripting/extension environment. These users will have received training for operating the TPS software including the execution of these scripts.

This section enumerates the types of device users, describe their characteristics, and why they are interested in the device [[FDA-HFE:5.1]].

## Medical Physics Specialist (MP)

The Medical Physics Specialist will typically be responsible for performing Quality Assurance (QA) of a patient's radiotherapy treatment plan. Scripts provided will help them automate many of these checks. In addition, they are also responsible for the installation of these scripts and must ensure they are operating properly.

## Radiation Therapist (RT)

A Radiation Therapist's responsibilities include contouring of structures defining patient anatomy using the TPS as well as generating the treatment plan. Scripts can automate parts of this workflow and can also be used for automated checks before being passed on to the MP for QA.

## Radiation Oncologist (RO)

ROs will often contour specific structures, usually defining the target volume to receive the radiation dose which they prescribed. They must also check the treatment plan to ensure the treatment delivers their prescribed dose and is safe for the patient. Scripts can automate parts of this workflow.

# Use Environments

This section enumerates the environments in which the {{ device.name }} will be used [[FDA-HFE:5.2]].

## Users Office in Clinic

All users (MP, RT, RO) will most commonly use the TPS from their designated office at the clinic. In certain scenarios offices are shared so some background noise from other conversations in the office may occur. They will operate the TPS on a designated computer which has been assigned to them.

## Users Home

At times these users may work from home and operate the TPS via a Virtual Private Network (VPN) connection. They will be presented the exact same interface when operating the device from home, but may at times experience interface lag due to the VPN connection.

# Use Cases

## Medical Physicist Optimization Parameter QA Check

During the QA of a treatment plan a Medical Physicist must check the algorithm used for the calculation to confirm it was selected correctly based on the department protocol. In addition they must check that the grid size on which the calculation was done also conforms to the protocol.

## Problem Y

Brief description.

# Requirement Details
{% for requirement in requirements %}
## {{ requirement.title }}

*Requirement ID:* {{ requirement.id }}

{{ requirement.description }}
{% endfor %}

# Traceability Tables
{% if device.samd %}
## Software Requirements Table

[[ Each requirement has a unique id satisfying 62304:5.2.6.e]]
| ID | Title |
| --- | --- |
{%- for requirement in requirements %}
| {{ requirement.id }} | {{ requirement.title }} |
{%- endfor %}
{% else %}
## Software Requirements Table

| Soft. Req. ID | System Req. IDs | Title |
| --- | --- | --- |
{%- for requirement in requirements %}
| {{ requirement.id }} | {{ requirement.system_requirements|join(', ') }} | {{ requirement.title }} |
{%- endfor %}

## System Requirements Mapping

| System Req. ID | Soft. Req. IDs |
| --- | --- |
{%- for system_requirement_id, software_requirement_ids in requirements|invert_dependencies('id', 'system_requirements') %}
| {{ system_requirement_id }} | {{ software_requirement_ids|sort|join(', ') }} |
{%- endfor %}
{%- endif %}
