#!/bin/sh

exec < /dev/tty

# Function to display the main menu and select a module
select_module() {
  while true; do
    echo "A. Select Module/Functional Category:"
    echo "1. Account & User Management"
    echo "2. Account Management"
    echo "3. Allocation Management"
    echo "4. Allocation/Sourcing Management"
    echo "5. Certificate Configuration"
    echo "6. Contract Management"
    echo "7. Customer Management"
    echo "8. Dashboard"
    echo "9. Issue Reporting"
    echo "10. Logistic Management"
    echo "11. Product & Configuration"
    echo "12. Production Management"
    echo "13. Shipment Dashboard"
    echo "14. Shipment Management"
    echo "15. Sourcing & Contract Management"
    echo "16. Spatial Monitoring And Analysis"
    echo "17. Supplier Profile Management"
    echo "18. Task & Workflow Management"
    echo "19. Tenant Management"
    echo "20. Traceability Management"
    echo "21. Notification Management"
    echo "22. Others"
  
    read -p "Select Module/Functional Category (1-22): " module
  
    case $module in
      1) module_name="Account & User Management"; break;;
      2) module_name="Account Management"; break;;
      3) module_name="Allocation Management"; break;;
      4) module_name="Allocation/Sourcing Management"; break;;
      5) module_name="Certificate Configuration"; break;;
      6) module_name="Contract Management"; break;;
      7) module_name="Customer Management"; break;;
      8) module_name="Dashboard"; break;;
      9) module_name="Issue Reporting"; break;;
      10) module_name="Logistic Management"; break;;
      11) module_name="Product & Configuration"; break;;
      12) module_name="Production Management"; break;;
      13) module_name="Shipment Dashboard"; break;;
      14) module_name="Shipment Management"; break;;
      15) module_name="Sourcing & Contract Management"; break;;
      16) module_name="Spatial Monitoring And Analysis"; break;;
      17) module_name="Supplier Profile Management"; break;;
      18) module_name="Task & Workflow Management"; break;;
      19) module_name="Tenant Management"; break;;
      20) module_name="Traceability Management"; break;;
      21) module_name="Notification Management"; break;;
      22) module_name="Others"; break;;
      *) echo "Invalid module selection, please try again.";;
    esac
  done
  
  echo "You have selected: $module_name"
  
  # Call the next function based on the selection
  select_business_unit
}

exec < /dev/tty

# Function to select a business unit
select_business_unit() {
  while true; do
    echo "B. Select Business Unit:"
    echo "1. Tenant"
    echo "2. Customer"
    echo "3. KCP"
    echo "4. Mill"
    echo "5. Mill/KCP"
    echo "6. Platform Admin"
    echo "7. Platform Management"
    echo "8. Refinery"
    echo "9. Supply Chain Department"
    echo "10. Sustainability"
    echo "11. Tenant Admin"

    read -p "Select Business Unit (1-11): " business_unit
  
    case $business_unit in
      1) business_unit_name="Tenant"; break;;
      2) business_unit_name="Customer"; break;;
      3) business_unit_name="KCP"; break;;
      4) business_unit_name="Mill"; break;;
      5) business_unit_name="Mill/KCP"; break;;
      6) business_unit_name="Platform Admin"; break;;
      7) business_unit_name="Platform Management"; break;;
      8) business_unit_name="Refinery"; break;;
      9) business_unit_name="Supply Chain Department"; break;;
      10) business_unit_name="Sustainability"; break;;
      11) business_unit_name="Tenant Admin"; break;;
      *) echo "Invalid business unit selection, please try again.";;
    esac
  done
  
  echo "You have selected: $business_unit_name"
  
  # Call the next function
  enter_use_case
}

# Function to enter use case ID and JIRA Issue No
enter_use_case() {
  read -p "C. Enter Use Case ID: " use_case_id
  read -p "D. Enter JIRA Issue No: " jira_issue_no
  read -p "E. Provide Change Summary (max 50 words): " change_summary
  
  # Check word count for change summary
  word_count=$(echo "$change_summary" | wc -w)
  if [ "$word_count" -gt 50 ]; then
    echo "Error: Change Summary exceeds 50 words."
    exit 1
  fi

  # Construct commit message
  commit_message="[${module_name}] - [${business_unit_name}] - [${use_case_id}] - [${jira_issue_no}] - ${change_summary}"

  # Set the commit message
  echo $commit_message

  echo "$commit_message" > .git/COMMIT_EDITMSG

  # Validate the commit message format
  validate_commit_message "$commit_message"
}

# Function to validate the commit message
validate_commit_message() {
  commit_message="$1"

  # Define regex to match the commit message format
  regex="^\[[^]]+\] - \[[^]]+\] - \[[^]]+\] - \[[^]]+\] - .+$"

  # Check if commit message matches the required format
  if ! echo "$commit_message" | grep -qE "$regex"; then
    echo "ERROR: Commit message does not follow the required format:"
    echo "[Module/Functional Category] - [Business Unit] - [Use Case ID] - [JIRA Issue No] - [Change Summary]"
    exit 1
  fi

  # If all checks pass, proceed with the commit
  echo "All checks passed. Proceeding with the commit."
  exit 0
}

# Call the first function to start the chain
select_module
