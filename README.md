# Troubleshooting Scenarios - Home Lab

## Overview
Real troubleshooting cases performed in a home lab environment using Windows Server 2022 and Windows 10.

## Case 1: Windows 10 Client Could Not Join Domain

**Problem:** Windows 10 (HELPDESK-01) could not join lab.local domain — ERROR_TIMEOUT

**Symptoms:**
- Error: "An Active Directory Domain Controller for the domain lab.local could not be contacted"
- ping to server IP (192.168.1.10) was successful
- DNS query was timing out

**Root Cause:** 
Both VMs were on different VMware networks:
- Server: Custom VMnet0 (192.168.1.10)
- Client: NAT (192.168.40.129) — different subnet

**Steps Taken:**
1. Ran ipconfig on both VMs — identified different subnets
2. Checked VMware Network Adapter settings
3. Changed Client VM from NAT to Custom VMnet0
4. Set static IP on client: 192.168.1.20
5. Set DNS to point to Server: 192.168.1.10
6. Rejoined domain successfully

**Result:** HELPDESK-01 successfully joined lab.local domain ✅

---

## Case 2: CMD Requires Elevation

**Problem:** netsh commands failed with "requires elevation"

**Solution:** Ran CMD as Administrator

**Result:** Commands executed successfully ✅
