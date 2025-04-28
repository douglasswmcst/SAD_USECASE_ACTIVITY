# **Use Case Descriptions**  
## **Stationery Store Inventory System**  

---

### **Use Case 1: Submit Stationery Request**  
**1. Brief Description**  
An employee submits a request for stationery items through the system.  

**2. Flow of Events**  
#### **Basic Flow:**  
1. Employee logs into the system.  
2. Employee selects "Create New Request."  
3. System displays the stationery catalogue.  
4. Employee selects items and enters quantities.  
5. Employee submits the request.  
6. System validates the request (checks item availability).  
7. System saves the request with status "Pending Approval."  
8. System notifies the Department Head by calling **Notify Request Status**.  
9. Use Case terminates.  

#### **Alternate Flow:**  
- **A1: Item out of stock**  
  6a. System detects insufficient stock for an item.  
  7a. System notifies the Employee and suggests alternatives.  
  8a. Use Case resumes at Step 4.  

**3. Special Requirements**  
- Catalogue must load within 2 seconds.  
- Mobile-responsive interface.  

**4. Preconditions**  
- Employee is authenticated.  
- Stationery catalogue is up to date.  

**5. Postconditions**  
- Request is saved with status "Pending Approval."  

**6. Extension Points**  
- Extends **Notify Request Status** if submission fails.  

---

### **Use Case 2: Approve Stationery Request**  
**1. Brief Description**  
A Department Head reviews and approves/rejects stationery requests.  

**2. Flow of Events**  
#### **Basic Flow:**  
1. Department Head logs into the system.  
2. System displays a list of pending requests.  
3. Department Head selects a request to review.  
4. System shows request details (items, quantities, requester).  
5. Department Head approves the request.  
6. System updates the request status to "Approved."  
7. System notifies the Employee by calling **Notify Request Status**.  
8. Use Case terminates.  

#### **Alternate Flow:**  
- **A1: Request rejected**  
  5a. Department Head rejects the request and enters comments.  
  6a. System updates status to "Rejected" and stores comments.  
  7a. System notifies the Employee by calling **Notify Request Status**.  

**3. Special Requirements**  
- Audit trail for approval decisions.  

**4. Preconditions**  
- Request is in "Pending Approval" status.  

**5. Postconditions**  
- Request status is updated to "Approved" or "Rejected."  

**6. Extension Points**  
- Extends **Notify Request Status**.  

---

### **Use Case 3: Process Requisition**  
**1. Brief Description**  
The Store Clerk processes approved requests and prepares disbursement.  

**2. Flow of Events**  
#### **Basic Flow:**  
1. Store Clerk logs into the system.  
2. System displays approved requests grouped by department.  
3. Clerk selects "Process Requisition."  
4. System generates a **Stationery Retrieval Form** (calls **Generate Retrieval Form**).  
5. System updates inventory levels by calling **Update Inventory**.  
6. System generates a **Disbursement List** (calls **Generate Disbursement List**).  
7. System notifies Department Representatives by calling **Notify Request Status**.  
8. Use Case terminates.  

**3. Special Requirements**  
- Supports batch processing for weekly requisitions.  

**4. Preconditions**  
- At least one request is approved.  

**5. Postconditions**  
- Retrieval and Disbursement forms are generated.  
- Inventory levels are updated.  

**6. Extension Points**  
- Includes **Generate Retrieval Form**, **Update Inventory**, and **Generate Disbursement List**.  

---

### **Use Case 4: Generate Retrieval Form**  
**1. Brief Description**  
System generates a list of items to retrieve from the warehouse.  

**2. Flow of Events**  
#### **Basic Flow:**  
1. Store Clerk selects "Generate Retrieval Form."  
2. System aggregates items from all approved requests.  
3. System sorts items by warehouse bin locations.  
4. System generates a printable Retrieval Form (PDF/print).  
5. Use Case terminates.  

**3. Special Requirements**  
- Form must be exportable to PDF.  

**4. Preconditions**  
- Approved requests exist.  

**5. Postconditions**  
- Retrieval Form is saved in the system.  

**6. Extension Points**  
- None.  

---

### **Use Case 5: Update Inventory**  
**1. Brief Description**  
System updates inventory levels after disbursement.  

**2. Flow of Events**  
#### **Basic Flow:**  
1. Store Clerk confirms disbursement is complete.  
2. System deducts disbursed quantities from inventory.  
3. System checks stock levels against thresholds.  
4. If stock is low, System triggers a restock alert by calling **Notify Request Status**.  
5. Use Case terminates.  

**3. Special Requirements**  
- Real-time sync with warehouse database.  

**4. Preconditions**  
- Items are physically disbursed.  

**5. Postconditions**  
- Inventory records reflect current stock.  

**6. Extension Points**  
- Extends **Notify Request Status** for low-stock alerts.  

---

### **Use Case 6: Generate Disbursement List**  
**1. Brief Description**  
System creates a list of items to deliver to each department.  

**2. Flow of Events**  
#### **Basic Flow:**  
1. Store Clerk selects "Generate Disbursement List."  
2. System groups items by department and collection point.  
3. System includes a section for recipient acknowledgment.  
4. System generates the Disbursement List (PDF/print).  
5. Use Case terminates.  

**3. Special Requirements**  
- List must include delivery dates/times.  

**4. Preconditions**  
- Retrieval Form is generated.  

**5. Postconditions**  
- Disbursement List is ready for delivery.  

**6. Extension Points**  
- None.  

---

### **Use Case 7: Notify Request Status**  
**1. Brief Description**  
System notifies users about request status changes.  

**2. Flow of Events**  
#### **Basic Flow:**  
1. System detects a status change (e.g., approval, rejection).  
2. System retrieves recipient details (Employee/Department Rep).  
3. System sends an email/in-app notification with the updated status.  
4. Use Case terminates.  

**3. Special Requirements**  
- Customizable email templates.  

**4. Preconditions**  
- A status change occurs.  

**5. Postconditions**  
- Users receive the latest status.  

**6. Extension Points**  
- None.  

---

### **Use Case 8: Acknowledge Receipt**  
**1. Brief Description**  
Department Representative confirms receipt of stationery.  

**2. Flow of Events**  
#### **Basic Flow:**  
1. Department Representative logs into the system or signs physically.  
2. System displays the Disbursement List for acknowledgment.  
3. Representative confirms received items and quantities.  
4. System records the acknowledgment.  
5. System updates the request status to "Completed."  
6. Use Case terminates.  

#### **Alternate Flow:**  
- **A1: Discrepancy in quantity**  
  3a. Representative notes missing items.  
  4a. System flags the request for Store Clerk review.  
  5a. System notifies the Store Clerk by calling **Notify Request Status**.  

**3. Special Requirements**  
- Supports digital signatures.  

**4. Preconditions**  
- Delivery is completed.  

**5. Postconditions**  
- Request is marked "Completed."  

**6. Extension Points**  
- None.  

---