# Infrastructure Backup Documentation

## Introduction

This document provides a comprehensive overview of the backup strategy for our infrastructure, including virtual machines (pavroto-1 and pavroto-2) and critical services. Effective backup procedures are essential for data security, disaster recovery, and business continuity.

## Backup Components

### Services

#### MySQL Database (pavroto-2)
- **Purpose:** Stores user data from Agama.
- **Backup Frequency:** Hourly.
- **Backup Method:** Automated database dumps (mysqldump).
- **Retention Policy:** Store hourly backups for 7 days.
- **Backup Coverage:** Database data and schema are backed up.

#### InfluxDB (pavroto-2)
- **Purpose:** Stores latency information and logs.
- **Backup Frequency:** Hourly.
- **Backup Method:** Use `influxd backup` command.
- **Retention Policy:** Store daily backups for 14 days.
- **Backup Coverage:** InfluxDB data and configurations are backed up.

#### Ansible Repository
- **Purpose:** Infrastructure as Code (IaC).
- **Backup Frequency:** On code change.
- **Backup Method:** Version control with Git.
- **Retention Policy:** Maintain a full history.
- **Backup Coverage:** All Ansible code, playbooks, and roles are backed up.

## Backup Server

### Backup Server (backup.pavroto.ttu)
- **Purpose:** Dedicated server for backup storage.
- **Location:** Offsite or separate from primary infrastructure.
- **Security:** Implement strict access controls and encryption.

## Recovery Objectives

### RPO (Recovery Point Objective)
- The maximum tolerable data loss is defined as:
  - For services: Up to 1 hour.
  - For the Ansible repository: Immediate.

### RTO (Recovery Time Objective)
- The maximum tolerable downtime for infrastructure and services is defined as:
  - For VMs and services: Up to 1 hour.
  - For the Ansible repository: Immediate availability.

## Disaster Recovery

In the event of infrastructure failure or data loss, the following disaster recovery procedures should be followed:

1. Restore Virtual Machines:
   - Recreate pavroto-1 and pavroto-2 using automated provisioning and configuration management tools (e.g., Ansible).

2. Database and InfluxDB:
   - Restore from the most recent backup on the backup server.

3. Ansible Repository:
   - Clone the Ansible repository from the version control system.

## Monitoring and Testing

- Regularly monitor backup processes and ensure that backups are completed successfully.
- Periodically test the restoration of backups to validate the data recovery process.

## Usability Checks

- Backup usability is verified through periodic restoration tests to ensure that backups can be successfully restored.

## Restoration Criteria

- Backups should be restored in the following scenarios:
  - Data corruption or loss.
  - Infrastructure failure.
  - Significant code or configuration errors.

## Conclusion

A well-defined backup strategy is essential for ensuring data integrity and the resilience of our infrastructure. This documentation serves as a reference for backup procedures, retention policies, and disaster recovery processes.

Please note that this document is a template and should be customized to reflect the specifics of your infrastructure and organizational requirements.
