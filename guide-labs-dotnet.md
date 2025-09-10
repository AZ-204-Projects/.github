# PowerShell Deployment Script Style Guide - Tutorial Edition

## 📋 Core Principles for Educational Deployments

### 1. **Learning Over Efficiency**
- Prioritize information exposure over performance optimization
- Show intermediate steps and results for educational value
- Include "What we're doing and why" explanations
- Provide detailed error context for troubleshooting skills
- Display resource relationships and dependencies

### 2. **Centralized Educational Configuration**
- Single `config.ps1` file with all settings and learning toggles
- Educational comments explaining naming patterns and constraints
- Cost awareness indicators throughout
- Variable naming that teaches Azure concepts
- Validation functions with instructional feedback

### 3. **Enhanced Error Handling for Learning**
- Check `$LASTEXITCODE` after every Azure CLI call with detailed explanations
- Transform errors into learning opportunities
- Show common failure patterns and solutions
- Validate prerequisites with educational context
- Provide actionable error messages with troubleshooting guidance

### 4. **Rich Educational Feedback**
- Color-coded output with concept reinforcement
- Progress indicators with resource details
- Cost implications at decision points
- Security consideration highlights
- Intermediate value displays for understanding

### 5. **Safety and Learning Validation**
- Check resource existence with relationship explanations
- Validate tool availability with version information
- Confirm destructive operations with cost awareness
- Test connectivity with troubleshooting context

## 🛠️ Educational Script Structure Template

```powershell
# [NN-script-name.ps1]
# [Brief description of what this script does and learning objectives]
# Dependencies: [List required tools, previous scripts, concepts]

. .\config.ps1

Write-Host "[Action Description]..." -ForegroundColor Yellow

# [Step 1: Educational Prerequisites]
Write-Host "Validating prerequisites and explaining requirements..." -ForegroundColor Cyan
# Validation logic with educational context
# Tool version displays and explanations

# [Step 2: Concept Introduction]
if ($EXPLAIN_CONCEPTS) {
    Write-Host ""
    Write-Host "=== What We're About To Do ===" -ForegroundColor Magenta
    # Explain the upcoming operations and their purpose
    Write-Host "===============================" -ForegroundColor Magenta
}

# [Step 3: Main Operations with Learning Details]
Write-Host "Performing main operations with detailed feedback..." -ForegroundColor Cyan
# Core functionality with progress updates and intermediate results

# [Step 4: Educational Verification]
Write-Host "Verifying results and explaining what we created..." -ForegroundColor Cyan
# Test and validate outcomes with educational context

# [Step 5: Learning Reinforcement]
if ($EXPLAIN_CONCEPTS) {
    Write-Host ""
    Write-Host "=== What We Just Accomplished ===" -ForegroundColor Magenta
    # Summarize key concepts and next steps
    Write-Host "==================================" -ForegroundColor Magenta
}

# [Final Educational Summary]
Write-Host ""
Write-Host "=== [Operation] Complete ===" -ForegroundColor Green
# Key outputs, URLs, next steps, cost reminders
Write-Host "================================" -ForegroundColor Green
```

## 🎨 Educational Output Formatting Standards

### Enhanced Color Usage
```powershell
Write-Host "Main step descriptions" -ForegroundColor Yellow
Write-Host "  Sub-actions and progress details" -ForegroundColor Cyan
Write-Host "✓ Success confirmations with details" -ForegroundColor Green
Write-Host "💡 Learning concepts and explanations" -ForegroundColor Magenta
Write-Host "💰 Cost implications and awareness" -ForegroundColor Yellow
Write-Host "🔒 Security considerations" -ForegroundColor Yellow
Write-Warning "Non-fatal warnings with educational context"
Write-Error "Fatal errors with troubleshooting guidance"
Write-Host "  Technical details and resource properties" -ForegroundColor Gray
```

### Educational Section Headers
```powershell
Write-Host ""
Write-Host "=== What We're About To Do ===" -ForegroundColor Magenta
Write-Host "We'll create an App Service Plan, which is like renting server space"
Write-Host "===============================" -ForegroundColor Magenta

Write-Host ""
Write-Host "💰 Cost Impact Analysis" -ForegroundColor Yellow
Write-Host "This operation will cost approximately $X/month"
Write-Host "========================" -ForegroundColor Yellow
```

### Enhanced Progress Indicators
```powershell
Write-Host "✓ App Service Plan created successfully" -ForegroundColor Green
Write-Host "  Name: $SERVICE_PLAN_NAME" -ForegroundColor Gray
Write-Host "  SKU: $SERVICE_PLAN_SKU (~$XX/month)" -ForegroundColor Gray
Write-Host "  Resource ID: $resourceId" -ForegroundColor Gray

Write-Host "⚠️ Resource already exists - this is normal for learning labs" -ForegroundColor Yellow
Write-Host "❌ Operation failed - let's understand why" -ForegroundColor Red
```

## 🔧 Educational Configuration Patterns

### Learning Control Variables
```powershell
# =================================
# LEARNING CONFIGURATION
# =================================
$EXPLAIN_CONCEPTS = $true         # Show "What we're doing and why" sections
$SHOW_INTERMEDIATE = $true        # Display intermediate values and resource IDs
$COST_AWARENESS = $true           # Highlight cost implications throughout
$SECURITY_FOCUS = $true           # Emphasize security best practices
$TROUBLESHOOTING_MODE = $false    # Extra verbose output for debugging
```

### Educational Variable Naming with Context
```powershell
# =================================
# CORE RESOURCE NAMING
# =================================
$PROJECT_NAME = "learningtodo"        # Keep short - used in many resource names
$DISCRIMINATOR = "demo123"            # Makes resources globally unique (change this!)
$LOCATION = "East US"                 # Azure region for all resources

# Why these naming patterns?
# • Short names avoid Azure's length limits (24 chars for storage, 63 for many others)
# • Discriminator prevents conflicts when multiple people do this tutorial
# • Consistent location reduces data transfer costs and latency

# =================================
# APPLICATION ARCHITECTURE
# =================================
$RG_NAME = "$PROJECT_NAME-rg"                    # Resource Group (logical container)
$SERVICE_PLAN_NAME = "$PROJECT_NAME-plan"        # App Service Plan (compute resources)
$API_APP_NAME = "$PROJECT_NAME-api"              # Backend REST API application
$WEB_APP_NAME = "$PROJECT_NAME-web"              # Frontend web application

# Generated names with global uniqueness requirements
$API_SERVICE_NAME = "$API_APP_NAME-$DISCRIMINATOR"     # Must be globally unique
$WEB_SERVICE_NAME = "$WEB_APP_NAME-$DISCRIMINATOR"     # Must be globally unique
$DB_SERVER_NAME = "$PROJECT_NAME-sql-$DISCRIMINATOR"   # SQL Server (globally unique)
$STORAGE_ACCOUNT_NAME = "${PROJECT_NAME}storage$DISCRIMINATOR"  # Storage (no dashes, globally unique)

# =================================
# SERVICE CONFIGURATION WITH LEARNING CONTEXT
# =================================
$SERVICE_PLAN_SKU = "F1"              # F1 = Free tier (great for learning!)
$SQL_TIER = "Basic"                   # Basic = $5/month (cheapest paid option)
$DOTNET_VERSION = "9.0"               # Latest LTS version of .NET
$BUILD_CONFIGURATION = "Release"      # Optimized builds for deployment

# SKU Education:
# • F1 (Free): Perfect for tutorials, has limitations (60 CPU minutes/day)
# • B1 (Basic): $15/month, no daily limits, good for small projects
# • S1 (Standard): $75/month, includes staging slots and custom domains
```

### Educational Validation Functions
```powershell
function Test-GlobalUniqueness {
    param(
        [string]$ServiceName, 
        [string]$Type = "webapp"
    )
    
    Write-Host "  Checking if '$ServiceName' is globally available..." -ForegroundColor Cyan
    
    $available = switch ($Type) {
        "webapp" { 
            $result = az webapp show --name $ServiceName --query "name" -o tsv 2>$null
            $null -eq $result
        }
        "sql" {
            $result = az sql server show --name $ServiceName --resource-group "dummy" --query "name" -o tsv 2>$null
            $null -eq $result
        }
        "storage" {
            $result = az storage account check-name --name $ServiceName --query "nameAvailable" -o tsv 2>$null
            $result -eq "true"
        }
    }
    
    if ($available) {
        Write-Host "  ✓ '$ServiceName' is available" -ForegroundColor Green
        if ($EXPLAIN_CONCEPTS) {
            Write-Host "    Global uniqueness means no one else in the world can use this name" -ForegroundColor Gray
            Write-Host "    That's why we use discriminators like '$DISCRIMINATOR'" -ForegroundColor Gray
        }
    } else {
        Write-Host "  ❌ '$ServiceName' is already taken globally" -ForegroundColor Red
        Write-Host "    Try changing your discriminator in config.ps1" -ForegroundColor Gray
    }
    
    return $available
}

function Test-Prerequisites {
    param([switch]$ShowDetails)
    
    Write-Host "Checking required tools and permissions..." -ForegroundColor Cyan
    $allGood = $true
    
    # Azure CLI
    try {
        $azVersion = az version --query '"azure-cli"' -o tsv 2>$null
        if ($azVersion) {
            Write-Host "✓ Azure CLI available: $azVersion" -ForegroundColor Green
            if ($ShowDetails -and $EXPLAIN_CONCEPTS) {
                Write-Host "  The Azure CLI is our primary tool for managing Azure resources" -ForegroundColor Gray
            }
        } else {
            throw "Not found"
        }
    } catch {
        Write-Host "❌ Azure CLI not found" -ForegroundColor Red
        Write-Host "  Install from: https://docs.microsoft.com/en-us/cli/azure/install-azure-cli" -ForegroundColor Gray
        $allGood = $false
    }
    
    # .NET SDK
    try {
        $dotnetVersion = dotnet --version 2>$null
        if ($dotnetVersion) {
            Write-Host "✓ .NET SDK available: $dotnetVersion" -ForegroundColor Green
            if ($ShowDetails -and $EXPLAIN_CONCEPTS) {
                Write-Host "  We need this to build your .NET applications" -ForegroundColor Gray
            }
        } else {
            throw "Not found"
        }
    } catch {
        Write-Host "❌ .NET SDK not found" -ForegroundColor Red
        Write-Host "  Install from: https://dotnet.microsoft.com/download" -ForegroundColor Gray
        $allGood = $false
    }
    
    # Azure Login Status
    try {
        $account = az account show --query "name" -o tsv 2>$null
        if ($account) {
            Write-Host "✓ Logged into Azure: $account" -ForegroundColor Green
            if ($ShowDetails -and $EXPLAIN_CONCEPTS) {
                Write-Host "  This determines which subscription will be billed for resources" -ForegroundColor Gray
            }
        } else {
            throw "Not logged in"
        }
    } catch {
        Write-Host "❌ Not logged into Azure" -ForegroundColor Red
        Write-Host "  Run: az login" -ForegroundColor Gray
        $allGood = $false
    }
    
    return $allGood
}
```

## 🛡️ Educational Error Handling Patterns

### Enhanced Azure CLI Error Context
```powershell
Write-Host "Creating Resource Group..." -ForegroundColor Cyan
$lastCommand = "resource group create --name $RG_NAME --location '$LOCATION'"
az $lastCommand.Split(' ')
if ($LASTEXITCODE -ne 0) {
    Write-Host "❌ Failed to create Resource Group" -ForegroundColor Red
    Write-Host "  Command attempted: az $lastCommand" -ForegroundColor Gray
    Write-Host "  Exit code: $LASTEXITCODE" -ForegroundColor Gray
    Write-Host "  Common causes:" -ForegroundColor Gray
    Write-Host "    • Insufficient permissions (need Contributor role)" -ForegroundColor Gray
    Write-Host "    • Invalid location name (try 'East US' instead of 'eastus')" -ForegroundColor Gray
    Write-Host "    • Subscription quota limits reached" -ForegroundColor Gray
    Write-Host "  Troubleshooting:" -ForegroundColor Gray
    Write-Host "    • Check: az account list-locations --query '[].name' -o table" -ForegroundColor Gray
    Write-Host "    • Verify: az account show --query 'user.name' -o tsv" -ForegroundColor Gray
    throw "Cannot proceed without Resource Group"
}
Write-Host "✓ Resource Group '$RG_NAME' created in $LOCATION" -ForegroundColor Green

if ($COST_AWARENESS) {
    Write-Host "  💰 Resource Groups are free - they're just organizational containers" -ForegroundColor Gray
}
```

### Educational Try-Catch Patterns
```powershell
Write-Host "Testing application startup..." -ForegroundColor Cyan
try {
    $response = Invoke-WebRequest -Uri "https://$API_SERVICE_NAME.azurewebsites.net/health" -TimeoutSec 30 -UseBasicParsing
    Write-Host "✓ API is responding successfully" -ForegroundColor Green
    Write-Host "  Status: $($response.StatusCode)" -ForegroundColor Gray
    Write-Host "  Response time: $($response.ResponseTime)ms" -ForegroundColor Gray
    
    if ($EXPLAIN_CONCEPTS) {
        Write-Host "  💡 Health endpoints are crucial for monitoring" -ForegroundColor Magenta
        Write-Host "     Azure uses them to determine if your app is working" -ForegroundColor Gray
    }
} catch {
    Write-Host "⚠️ API not yet responding (this is normal)" -ForegroundColor Yellow
    Write-Host "  Apps can take 2-5 minutes to fully start up" -ForegroundColor Gray
    Write-Host "  You can monitor startup at: https://$API_SERVICE_NAME.scm.azurewebsites.net" -ForegroundColor Gray
    
    if ($TROUBLESHOOTING_MODE) {
        Write-Host "  Error details: $($_.Exception.Message)" -ForegroundColor Gray
    }
}
```

## 📦 Educational File Organization Standards

### Learning-Focused Naming Convention
```
config.ps1                          # Central configuration with educational comments
01-create-infrastructure.ps1        # Infrastructure with concept explanations
02-build-applications.ps1           # Build process with detailed output
03-deploy-api.ps1                   # API deployment with testing
04-deploy-web.ps1                   # Web app deployment with configuration
05-configure-database.ps1           # Database setup with security focus
deploy-all.ps1                      # Complete pipeline with learning checkpoints
test-deployment.ps1                 # Validation and troubleshooting
99-cleanup-resources.ps1            # Cleanup with cost impact explanation
README.md                          # Learning objectives and prerequisites
```

### Educational Bicep Integration
```powershell
# Deploy infrastructure with educational output
Write-Host "Deploying infrastructure using Bicep..." -ForegroundColor Yellow
if ($EXPLAIN_CONCEPTS) {
    Write-Host "💡 Bicep is Azure's Infrastructure as Code language" -ForegroundColor Magenta
    Write-Host "   It's like JSON templates but much more readable" -ForegroundColor Gray
    Write-Host "   Everything we create is versioned and repeatable" -ForegroundColor Gray
}

$deploymentName = "infrastructure-$(Get-Date -Format 'yyyyMMdd-HHmmss')"
az deployment group create `
    --resource-group $RG_NAME `
    --template-file "./bicep/main.bicep" `
    --parameters projectName=$PROJECT_NAME discriminator=$DISCRIMINATOR location=$LOCATION `
    --name $deploymentName

if ($LASTEXITCODE -eq 0) {
    Write-Host "✓ Infrastructure deployment completed" -ForegroundColor Green
    
    # Show what was created
    if ($SHOW_INTERMEDIATE) {
        Write-Host "  Resources created:" -ForegroundColor Gray
        az deployment group show --resource-group $RG_NAME --name $deploymentName --query "properties.outputs" -o table
    }
} else {
    Write-Host "❌ Bicep deployment failed" -ForegroundColor Red
    Write-Host "  Common Bicep issues:" -ForegroundColor Gray
    Write-Host "    • Template syntax errors" -ForegroundColor Gray
    Write-Host "    • Parameter validation failures" -ForegroundColor Gray
    Write-Host "    • Resource naming conflicts" -ForegroundColor Gray
    Write-Host "  Check deployment details:" -ForegroundColor Gray
    Write-Host "    az deployment group show --resource-group $RG_NAME --name $deploymentName" -ForegroundColor Gray
    throw "Infrastructure deployment required to continue"
}
```

## 🎯 Educational User Experience Patterns

### Learning-Rich Summary Displays
```powershell
Write-Host ""
Write-Host "=== Deployment Learning Summary ===" -ForegroundColor Green
Write-Host "🏗️  Infrastructure:" -ForegroundColor Yellow
Write-Host "   Resource Group: $RG_NAME (organizes all resources)" -ForegroundColor Gray
Write-Host "   App Service Plan: $SERVICE_PLAN_NAME ($SERVICE_PLAN_SKU tier)" -ForegroundColor Gray
Write-Host "   SQL Server: $DB_SERVER_NAME (managed database service)" -ForegroundColor Gray

Write-Host ""
Write-Host "🌐 Application URLs:" -ForegroundColor Yellow
Write-Host "   API: https://$API_SERVICE_NAME.azurewebsites.net" -ForegroundColor Cyan
Write-Host "   Web: https://$WEB_SERVICE_NAME.azurewebsites.net" -ForegroundColor Cyan
Write-Host "   Database: $DB_SERVER_NAME.database.windows.net" -ForegroundColor Cyan

if ($COST_AWARENESS) {
    Write-Host ""
    Write-Host "💰 Monthly Cost Estimate:" -ForegroundColor Yellow
    Write-Host "   App Service Plan ($SERVICE_PLAN_SKU): $XX" -ForegroundColor Gray
    Write-Host "   SQL Database ($SQL_TIER): $XX" -ForegroundColor Gray
    Write-Host "   Total: ~$XX/month" -ForegroundColor Gray
    Write-Host "   💡 Run 99-cleanup-resources.ps1 to delete everything!" -ForegroundColor Yellow
}

Write-Host ""
Write-Host "🎓 What You Learned:" -ForegroundColor Magenta
Write-Host "   • How Azure App Services host web applications" -ForegroundColor Gray
Write-Host "   • Resource Groups organize related resources" -ForegroundColor Gray
Write-Host "   • Managed Identity provides secure database access" -ForegroundColor Gray
Write-Host "   • Application Insights monitors app performance" -ForegroundColor Gray

Write-Host ""
Write-Host "🚀 Next Steps:" -ForegroundColor Yellow
Write-Host "   1. Test your applications using the URLs above" -ForegroundColor Gray
Write-Host "   2. Explore the Azure portal to see your resources" -ForegroundColor Gray
Write-Host "   3. Try modifying the code and redeploying" -ForegroundColor Gray
Write-Host "   4. Review Application Insights for performance data" -ForegroundColor Gray
Write-Host "=======================================" -ForegroundColor Green
```

### Interactive Learning Elements
```powershell
# Educational confirmation for destructive operations
Write-Host "⚠️  This will DELETE all resources and STOP all charges" -ForegroundColor Yellow
Write-Host "💰 Current estimated monthly cost: ~$XX" -ForegroundColor Yellow
if ($EXPLAIN_CONCEPTS) {
    Write-Host ""
    Write-Host "💡 Why we clean up:" -ForegroundColor Magenta
    Write-Host "   Azure charges for resources even when not in use" -ForegroundColor Gray
    Write-Host "   Leaving resources running can result in unexpected bills" -ForegroundColor Gray
    Write-Host "   Always clean up learning environments!" -ForegroundColor Gray
}

do {
    $confirmation = Read-Host "Type 'DELETE' to confirm cleanup (or 'cancel' to abort)"
    if ($confirmation -eq 'cancel') {
        Write-Host "Cleanup cancelled - resources remain active" -ForegroundColor Yellow
        exit 0
    }
} while ($confirmation -ne 'DELETE')

# Educational choice for optional operations
Write-Host "🧹 Optional: Delete local build artifacts?" -ForegroundColor Cyan
if ($EXPLAIN_CONCEPTS) {
    Write-Host "   This removes temporary files created during the build process" -ForegroundColor Gray
    Write-Host "   Safe to delete - they'll be recreated on next build" -ForegroundColor Gray
}
$choice = Read-Host "Delete build artifacts? (y/N)"
if ($choice -eq 'y' -or $choice -eq 'Y') {
    # Cleanup with educational output
    Write-Host "Removing build artifacts..." -ForegroundColor Cyan
    Remove-Item "./api/bin" -Recurse -Force -ErrorAction SilentlyContinue
    Remove-Item "./api/obj" -Recurse -Force -ErrorAction SilentlyContinue
    Remove-Item "./web/build" -Recurse -Force -ErrorAction SilentlyContinue
    Write-Host "✓ Build artifacts cleaned" -ForegroundColor Green
}
```

## 🔍 Educational Testing and Verification

### Learning-Focused Connectivity Tests
```powershell
Write-Host "Testing application health and learning about monitoring..." -ForegroundColor Cyan

# API Health Check
Write-Host "  Checking API health endpoint..." -ForegroundColor Cyan
try {
    $apiResponse = Invoke-WebRequest -Uri "https://$API_SERVICE_NAME.azurewebsites.net/health" -TimeoutSec 30 -UseBasicParsing
    Write-Host "  ✓ API is responding (Status: $($apiResponse.StatusCode))" -ForegroundColor Green
    
    if ($SHOW_INTERMEDIATE) {
        Write-Host "    Response time: $($apiResponse.ResponseTime)ms" -ForegroundColor Gray
        Write-Host "    Content length: $($apiResponse.Content.Length) bytes" -ForegroundColor Gray
    }
    
    if ($EXPLAIN_CONCEPTS) {
        Write-Host "    💡 Health checks help Azure monitor your app" -ForegroundColor Magenta
        Write-Host "       If this endpoint fails, Azure can restart your app" -ForegroundColor Gray
    }
} catch {
    Write-Host "  ⚠️ API health check failed (app may still be starting)" -ForegroundColor Yellow
    Write-Host "    This is normal for the first 2-5 minutes after deployment" -ForegroundColor Gray
    Write-Host "    Monitor startup: https://$API_SERVICE_NAME.scm.azurewebsites.net" -ForegroundColor Gray
    
    if ($TROUBLESHOOTING_MODE) {
        Write-Host "    Error: $($_.Exception.Message)" -ForegroundColor Gray
    }
}

# Database Connectivity Test
Write-Host "  Testing database connectivity..." -ForegroundColor Cyan
try {
    $dbTest = az sql db show --name $DB_NAME --server $DB_SERVER_NAME --resource-group $RG_NAME --query "name" -o tsv 2>$null
    if ($dbTest) {
        Write-Host "  ✓ Database is accessible" -ForegroundColor Green
        
        if ($EXPLAIN_CONCEPTS) {
            Write-Host "    💡 We're using Managed Identity for secure access" -ForegroundColor Magenta
            Write-Host "       No passwords needed - Azure handles authentication" -ForegroundColor Gray
        }
    }
} catch {
    Write-Host "  ❌ Database connectivity issue" -ForegroundColor Red
    Write-Host "    Check firewall rules and managed identity configuration" -ForegroundColor Gray
}
```

### Educational Resource Verification
```powershell
function Test-ResourceDeployment {
    param([string]$ResourceType, [string]$ResourceName, [string]$ExpectedState = "Succeeded")
    
    Write-Host "Verifying $ResourceType deployment..." -ForegroundColor Cyan
    
    $resource = az resource show --name $ResourceName --resource-group $RG_NAME --resource-type $ResourceType --query "{name:name,state:properties.provisioningState,location:location}" -o json 2>$null
    
    if ($resource) {
        $resourceObj = $resource | ConvertFrom-Json
        if ($resourceObj.state -eq $ExpectedState) {
            Write-Host "✓ $ResourceType '$($resourceObj.name)' is ready" -ForegroundColor Green
            if ($SHOW_INTERMEDIATE) {
                Write-Host "  Location: $($resourceObj.location)" -ForegroundColor Gray
                Write-Host "  State: $($resourceObj.state)" -ForegroundColor Gray
            }
            return $true
        } else {
            Write-Host "⚠️ $ResourceType is in state: $($resourceObj.state)" -ForegroundColor Yellow
            return $false
        }
    } else {
        Write-Host "❌ $ResourceType '$ResourceName' not found" -ForegroundColor Red
        if ($EXPLAIN_CONCEPTS) {
            Write-Host "  This usually means:" -ForegroundColor Gray
            Write-Host "    • Deployment failed or is still in progress" -ForegroundColor Gray
            Write-Host "    • Resource name mismatch in configuration" -ForegroundColor Gray
            Write-Host "    • Insufficient permissions to view the resource" -ForegroundColor Gray
        }
        return $false
    }
}
```

## 📚 Educational Documentation Standards

### Learning-Focused Script Headers
```powershell
# 01-create-infrastructure.ps1
# Creates Azure infrastructure for a .NET web application tutorial
# 
# Learning Objectives:
#   • Understand Azure Resource Groups and organization
#   • Learn about App Service Plans and compute resources
#   • Explore Azure SQL Database managed services
#   • Practice Infrastructure as Code with Bicep
#
# Prerequisites:
#   • Azure CLI installed and authenticated
#   • Azure subscription with Contributor permissions
#   • Basic understanding of web application architecture
#
# Estimated Cost: $5-15/month (remember to run cleanup!)
# Estimated Time: 5-10 minutes
#
# Dependencies: 
#   • config.ps1 (must be configured first)
#   • ./bicep/main.bicep (infrastructure template)
```

### Educational Inline Comments
```powershell
# Create App Service Plan (the "server" that hosts web applications)
Write-Host "Creating App Service Plan..." -ForegroundColor Yellow
# App Service Plans determine CPU, memory, and features available to your apps
# Multiple web apps can share one plan to save costs
# F1 tier is free but has daily CPU minute limits - perfect for learning!
az appservice plan create --name $SERVICE_PLAN_NAME --resource-group $RG_NAME --sku $SERVICE_PLAN_SKU --location $LOCATION

if ($LASTEXITCODE -eq 0) {
    Write-Host "✓ App Service Plan created" -ForegroundColor Green
    if ($COST_AWARENESS) {
        Write-Host "  💰 $SERVICE_PLAN_SKU tier: Free (with limitations)" -ForegroundColor Gray
        Write-Host "     60 CPU minutes per day, 1GB disk space" -ForegroundColor Gray
    }
} else {
    throw "Failed to create App Service Plan - this is required for web apps"
}
```

### Educational Configuration Comments
```powershell
# =================================
# AZURE SQL CONFIGURATION
# =================================
$DB_SERVER_NAME = "$PROJECT_NAME-sql-$DISCRIMINATOR"  # Must be globally unique across ALL Azure
$DB_NAME = "TodoDatabase"                             # Simple name - only unique within server
$DB_ADMIN_USER = "sqladmin"                          # Admin username (avoid 'admin', 'sa', 'root')
$DB_SKU = "Basic"                                    # Basic = $5/month, good for learning
$DB_MAX_SIZE = "2GB"                                 # Basic tier allows up to 2GB

# SQL Server Naming Rules (why these constraints exist):
# • Must be globally unique (like domain names)
# • 3-63 characters, lowercase letters, numbers, hyphens only
# • Cannot start or end with hyphen
# • No consecutive hyphens
# This is why we use the discriminator pattern!

# Security Note:
# In production, never put passwords in config files
# We'll use Azure Key Vault and Managed Identity instead
```

---

