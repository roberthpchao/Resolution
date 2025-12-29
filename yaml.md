# **YAML Explained Simply**

**YAML** (YAML Ain't Markup Language) is a **human-friendly data format** that's easier to read and write than JSON or XML.

## **📊 Quick Comparison**

| Format | Example | Best For |
|--------|---------|----------|
| **YAML** | `name: John`<br>`age: 30` | Configuration files, readable data |
| **JSON** | `{"name": "John", "age": 30}` | APIs, data exchange |
| **XML** | `<person><name>John</name><age>30</age></person>` | Complex documents |

## **🎯 Why YAML for API Testing/Config?**

### **For Your Freelance Work:**
```yaml
# client_config.yaml - SUPER EASY TO READ
client: "Boutique Store"
api_url: "https://api.boutiquestore.com"
auth:
  type: "api_key"
  key: "sk_test_12345"
tests:
  - "health_check"
  - "checkout_flow"
  - "error_handling"
```

**Same in JSON:**
```json
{
  "client": "Boutique Store",
  "api_url": "https://api.boutiquestore.com",
  "auth": {
    "type": "api_key",
    "key": "sk_test_12345"
  },
  "tests": ["health_check", "checkout_flow", "error_handling"]
}
```

**YAML is cleaner and easier for clients to edit!**

## **📝 YAML Basics You Need**

### **1. Key-Value Pairs**
```yaml
# Simple values
name: "John Doe"
age: 30
is_active: true
price: 19.99
```

### **2. Lists/Arrays**
```yaml
# List of items (with dashes)
endpoints_to_test:
  - "/api/products"
  - "/api/cart"
  - "/api/users"

# Or inline
quick_tests: ["health", "auth", "cart"]
```

### **3. Nested Objects**
```yaml
# Hierarchical data
api_config:
  base_url: "https://api.example.com"
  timeout: 30
  retries: 3
  headers:
    content_type: "application/json"
    accept: "application/json"
```

### **4. Multi-line Strings**
```yaml
# For long text (like error messages)
description: |
  This API endpoint handles user registration.
  It expects email, password, and name fields.
  Returns 201 on success, 400 on validation error.
```

## **🔧 YAML in Your Freelance Project**

### **Client Configuration File:**
```yaml
# client_config.yaml
client: "Local Bakery"
project: "E-commerce API Testing"

# API Details
api:
  base_url: "https://api.localbakery.com"
  version: "v1"
  
  # Authentication (client fills this)
  authentication:
    type: "api_key"  # Options: api_key, bearer, basic, none
    api_key: "INSERT_API_KEY_HERE"
    # OR for bearer token:
    # type: "bearer"
    # token: "INSERT_TOKEN_HERE"
    
# What to test
test_scenarios:
  - "Basic connectivity"
  - "Product catalog"
  - "Shopping cart"
  - "User authentication"
  - "Checkout process"
  
# Test data
test_data:
  products:
    - id: 101
      name: "Sourdough Bread"
      price: 5.99
    - id: 102
      name: "Croissant"
      price: 3.50
      
# Special instructions
notes: |
  - Test environment only
  - Use test credit card: 4242 4242 4242 4242
  - API rate limit: 100 requests/minute
```

### **Test Results in YAML:**
```yaml
# test_results.yaml
test_run:
  date: "2024-01-15"
  api_tested: "https://api.localbakery.com"
  duration: "2 minutes 15 seconds"
  
results:
  total_tests: 15
  passed: 13
  failed: 2
  success_rate: 86.7%
  
failed_tests:
  - endpoint: "/api/checkout"
    issue: "Returns 500 error with invalid coupon"
    severity: "High"
    
  - endpoint: "/api/cart"
    issue: "Slow response (>2 seconds)"
    severity: "Medium"
    
recommendations:
  - "Fix coupon validation bug"
  - "Optimize cart endpoint performance"
  - "Add better error messages"
```

## **🐍 Reading YAML in Python**

### **Install pyyaml:**
```bash
pip install pyyaml
```

### **Simple Python Code:**
```python
import yaml

# 1. READ YAML file
with open('client_config.yaml', 'r') as file:
    config = yaml.safe_load(file)
    
print(f"Testing API: {config['api']['base_url']}")
print(f"Client: {config['client']}")

# 2. USE the config
api_url = config['api']['base_url']
auth_type = config['api']['authentication']['type']

# 3. WRITE YAML (save results)
results = {
    'test_run': {
        'date': '2024-01-15',
        'passed': 13,
        'failed': 2
    }
}

with open('test_results.yaml', 'w') as file:
    yaml.dump(results, file, default_flow_style=False)
```

## **🎯 Practical Example for Your Project**

### **File: `config_loader.py`**
```python
"""
Simple YAML config loader for freelance projects
"""
import yaml
import os

def load_client_config(config_file='client_config.yaml'):
    """Load client configuration from YAML"""
    if not os.path.exists(config_file):
        print(f"⚠️  Config file not found: {config_file}")
        print("Creating template...")
        create_template_config(config_file)
        return None
    
    with open(config_file, 'r') as f:
        config = yaml.safe_load(f)
    
    # Validate required fields
    required = ['client', 'api']
    for field in required:
        if field not in config:
            print(f"❌ Missing required field: {field}")
            return None
    
    print(f"✅ Loaded config for: {config['client']}")
    return config

def create_template_config(filename='client_config.yaml'):
    """Create a template config file for clients"""
    template = """# Client Configuration for API Testing
# Fill in the details below and save this file

client: "Your Company Name"
project: "API Testing Project"

# API Configuration
api:
  base_url: "https://api.yourcompany.com"
  
  # Choose ONE authentication method:
  authentication:
    # Method 1: API Key
    type: "api_key"
    api_key: "YOUR_API_KEY_HERE"
    
    # Method 2: Bearer Token (uncomment to use)
    # type: "bearer"
    # token: "YOUR_BEARER_TOKEN_HERE"
    
    # Method 3: Basic Auth (uncomment to use)
    # type: "basic"
    # username: "YOUR_USERNAME"
    # password: "YOUR_PASSWORD"

# Tests to run (uncomment what you need)
tests_to_run:
  - "health_check"
  - "product_catalog"
  # - "user_authentication"
  # - "shopping_cart"
  # - "checkout_flow"
  # - "error_handling"

# Test data
test_products:
  - id: 1
    name: "Test Product 1"
    price: 19.99
  - id: 2
    name: "Test Product 2"
    price: 29.99

# Notes for the tester
notes: |
  - This is a test/staging environment
  - Please don't use real customer data
  - API rate limit: 60 requests/minute
"""
    
    with open(filename, 'w') as f:
        f.write(template)
    
    print(f"📝 Template created: {filename}")
    print("Please fill in your details and run the tests again.")

# Usage
if __name__ == "__main__":
    config = load_client_config()
    if config:
        print(f"Will test: {config['api']['base_url']}")
```

## **🚀 Updated Freelance Workflow with YAML**

### **Step 1: Give Client Template**
```bash
# You give client this file:
python config_loader.py
# Creates: client_config.yaml (template)
```

### **Step 2: Client Fills It Out**
Client edits `client_config.yaml`:
```yaml
client: "Bob's Bookstore"
api:
  base_url: "https://api.bobsbooks.com"
  authentication:
    type: "api_key"
    api_key: "books_apikey_12345"
```

### **Step 3: You Run Tests**
```python
# Your script reads the YAML
config = load_client_config('client_config.yaml')

# Use the config
checker = EcommerceHealthCheck(
    base_url=config['api']['base_url'],
    auth_type=config['api']['authentication']['type'],
    api_key=config['api']['authentication']['api_key']
)
```

## **📊 YAML vs JSON **

| Feature | YAML | JSON |
|---------|------|------|
| **Readability** | ✅ Excellent (humans) | ⚠️ Okay (machines) |
| **Comments** | ✅ Yes (`# comment`) | ❌ No |
| **Client-friendly** | ✅ Very easy | ❌ Technical |
| **API use** | ❌ Rarely | ✅ Standard |
| **Config files** | ✅ Perfect | ⚠️ Acceptable |

## **🔧 Simple Alternative: Use JSON Instead**

If YAML feels complicated, just use JSON (which you already know):

**`client_config.json`:**
```json
{
  "client": "Local Store",
  "api": {
    "base_url": "https://api.example.com",
    "auth": {
      "type": "api_key",
      "key": "test_key_123"
    }
  }
}
```

**In Python:**
```python
import json
config = json.load(open('client_config.json'))
```

## **🎯 Recommendation for Your Project**

### **Keep it SIMPLE - Use JSON:**
1. **You already know JSON** from API responses
2. **Python has built-in JSON support** (no extra install)
3. **Clients can still edit it** (with a little guidance)
4. **Easier for you to maintain**

### **Simple JSON Config:**
```json
{
  "client_name": "Test Store",
  "api_url": "https://fakestoreapi.com",
  "auth_method": "none",
  "tests": ["health", "products", "cart"]
}
```
