---
title: Azure RBAC
aliases:
  - RBAC
draft: false
tags:
  - AZ-104
  - Cloud
  - Microsoft
author:
  - Sarthak Chandajkar
---
- **Azure RBAC** is an authorization system built on [[Azure Resource Manager]] that provides fine-grained access management for resources in Azure.
- grant the exact access that users need to do their jobs.


![[AZ RBAC.png]]

## Use Case Examples

- Allow one user to manage [[virtual machines]] in a subscription and another user to manage virtual networks.
- Allow a database administrator group to manage SQL databases in a subscription.
- Allow a user to manage all resources in a resource group, such as virtual machines, websites, and [[Subnets]].
- Allow an application to access all resources in a resource group.
- **IAM**: identity and access management

## How does it work?

- concept of **Role Assignments**
	1. Security Principle(who)
		- User
		- Group
		- Security Principle
	2. Role(what)
		- Owner
		- Contributor
		- Reader
		- User Access Administrator
		- Custom role
	3. Scope(where)
									 ![[Scope.png]]


> [!NOTE] Allow Model
> Azure RBAC is an _allow_ model. This means that when you're assigned a role, Azure RBAC allows you to perform certain actions such as read, write, or delete.
> 
>  If one role assignment grants you read permissions to a resource group, and a different role assignment grants you write permissions to the same resource group, then you'll have read and write permissions on that resource group.

- To view activity logs for RBAC changes, use [[Azure Activity Log]].
