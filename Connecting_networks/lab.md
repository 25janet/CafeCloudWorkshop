# Lab 1: VPC Peering and Connectivity

## Objectives
- Create a VPC peering connection
- Configure route tables to enable traffic flow
- Enable and analyze VPC Flow Logs
- Test connectivity across the peering connection

---

## Task 1: Create a VPC Peering Connection

1. Navigate to **VPC → Peering Connections**
2. Create a new peering connection
   - **Requester VPC**: Lab VPC
   - **Accepter VPC**: Shared VPC
   - Name the peering connection (e.g., `Lab-Peer`)
3. Send the peering request
4. Switch to the accepter VPC
5. Accept the peering request

---

## Task 2: Configure Route Tables

### Lab Public Route Table

| Destination | Target |
|------------|--------|
| 10.0.0.0/16 | local |
| 10.1.0.0/16 | VPC Peering Connection |
| 0.0.0.0/0 | Internet Gateway |

### Shared VPC Route Table

| Destination | Target |
|------------|--------|
| 10.1.0.0/16 | local |
| 10.0.0.0/16 | VPC Peering Connection |

---

## Task 3: Enable VPC Flow Logs

1. Go to **VPC → Your VPCs → Shared VPC**
2. Open the **Flow Logs** tab
3. Create a flow log with the following settings:
   - **Name**: `SharedVPCFlowLog`
   - **Filter**: All
   - **Maximum aggregation interval**: 1 minute
   - **Destination**: Send to CloudWatch Logs
   - **Log group**: `SharedVPCFlowLog`
   - **IAM role**: `vpc-flow-logs-role`
4. Create the flow log

---

## Task 4: Test the VPC Peering Connection

1. Use the **EC2 public IP** of the inventory application instance
2. Paste the public IP into your browser
3. Navigate to **Settings → Configure**
4. Enter the database connection details:
   - **Endpoint**: RDS endpoint
   - **Database**: inventory
   - **Username**: admin
   - **Password**: lab-password
5. Save the configuration

 Successful connection confirms that the VPC peering connection is working correctly and that routing is properly configured.

---

## Notes
- Ensure both VPCs have correct CIDR routes pointing to the peering connection
- VPC peering does not require an Internet Gateway
- Flow Logs help verify accepted and rejected traffic

