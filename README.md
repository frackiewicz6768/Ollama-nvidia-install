# Ollama-nvidia-install

Enumeration is the process of systematically gathering detailed information about a system, network, or application to understand its structure, resources, and configuration. It is a critical phase in both system administration and penetration testing, often following reconnaissance.
This document outlines methods for enumerating an organization’s network using different techniques. The focus is on utilizing manual and automatic enumerations.
Table of Contents

   1. Graphic card drivers installation
   2. Ollama installation
       - Requirements
       - Using dsquery
       - Using Graphical Interface
   3. Anythingllm installation
   4.  Additional Notes

## Manual enumeration

###  dsquery

The dsquery command-line tool is a powerful way to query Active Directory objects. 
To use dsquery, ensure RSAT is installed on your system. You can install it using the following PowerShell command:

    Get-WindowsCapability -Name RSAT* -Online

Common Commands

List all users in the domain:

    dsquery user -name *

Find a specific user:

    dsquery user -name "John Doe"

List all groups in the domain:

    dsquery group -name *

List all computers in the domain:

    dsquery computer -name *

Using Graphical Interface

If RSAT is not installed, you can use the graphical query window provided by rundll32.exe to enumerate objects in Active Directory.
Steps to Use the Graphical Interface
