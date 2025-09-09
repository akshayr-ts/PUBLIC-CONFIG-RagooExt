# Multi-Organization Pipeline Configuration

This extension now supports organization-specific pipeline configurations for multiple Zoho Recruit organizations.

## Organization Mapping

### Talent-Shore Organization

- **Organization ID**: `801559407`
- **Domain**: `.com` (recruit.zoho.com)
- **Configuration File**: `pipeline-config.json`
- **GitHub URL**: `https://raw.githubusercontent.com/akshayr-ts/PUBLIC-CONFIG-RagooExt/refs/heads/main/pipeline-config.json`

### FlexSupport Organization

- **Organization ID**: `20103859259`
- **Domain**: `.eu` (recruit.zoho.eu)
- **Configuration File**: `v2-pipeline-config-org2.json`
- **GitHub URL**: `https://raw.githubusercontent.com/akshayr-ts/PUBLIC-CONFIG-RagooExt/refs/heads/main/v2-pipeline-config-org2.json`

### TeachNow Organization

- **Organization ID**: `20094154729`
- **Domain**: `.eu` (recruit.zoho.eu)
- **Configuration File**: `v2-pipeline-config-org3.json`
- **GitHub URL**: `https://raw.githubusercontent.com/akshayr-ts/PUBLIC-CONFIG-RagooExt/refs/heads/main/v2-pipeline-config-org3.json`

### Remote Choice Organization

- **Organization ID**: `20086425055`
- **Domain**: `.eu` (recruit.zoho.eu)
- **Configuration File**: `v2-pipeline-config-org4.json`
- **GitHub URL**: `https://raw.githubusercontent.com/akshayr-ts/PUBLIC-CONFIG-RagooExt/refs/heads/main/v2-pipeline-config-org4.json`

## Pipeline Stages for FlexSupport

The FlexSupport organization uses the following pipeline stages:

1. **Applied Stage (darkblue)**

   - Associated
   - Applied

2. **Shortlisted Stage (topaz-blue)**

   - Qualified

3. **Submissions Stage (violet)**

   - Submitted to client

4. **Interview Stage (chocolate)**

   - Interview-Scheduled

5. **Offered Stage (yellow)**

   - Offer made

6. **Hired Stage (lightgreen)**

   - Hired

7. **Rejected Stage (red)**

   - Unqualified
   - Rejected by client
   - Rejected for interview
   - Rejected

8. **Archived Stage (cadet)**
   - Archived

## Pipeline Stages for TeachNow

The TeachNow organization uses the following comprehensive pipeline stages:

1. **Applied Stage (coral)**

   - Applied
   - AI Applications

2. **Shortlisted Stage (yellow)**

   - Shortlisted
   - Call not answered

3. **Booked Stage (darkblue)**

   - Booked

4. **Awaiting Approval Stage (chocolate)**

   - Waiting for Placement Manager

5. **Approved Stage (lightgreen)**

   - Approved

6. **Offered Stage (yellow)**

   - Offer planned
   - Offer made
   - Offer accepted
   - Offer declined
   - Offer withdrawn

7. **Hired Stage (lightgreen)**

   - Hired

8. **Rejected Stage (red)**

   - Rejected
   - Rejected by Candidate
   - Rejected by School
   - Rejected by Placement Manager

9. **Archived Stage (cadet)**
   - Archived

## Pipeline Stages for Remote Choice

The Remote Choice organization uses the following comprehensive pipeline stages:

1. **Applied Stage (apple-blossom)**

   - Applied
   - AI Applications
   - AI Database
   - AI LinkedIn

2. **Shortlisted Stage (sheen-gold)**

   - Shortlisted
   - Call Not Answered

3. **Booked Stage (birdflower-green)**

   - Booked

4. **Submitted to Client Stage (darkgreen)**

   - Submitted to client

5. **Chase Video Stage (pink)**

   - Chase Video

6. **Interview Stage (topaz-blue)**

   - Interview-Scheduled

7. **Offered Stage (yellow)**

   - Offered

8. **Hired Stage (lightgreen)**

   - Hired

9. **Rejected Stage (red)**

   - Rejected
   - Rejected by client

10. **Archived Stage (cadet)**
    - Archived

## How It Works

1. The extension automatically detects which organization is being used based on:

   - Organization ID extracted from the URL path (`/org{ID}/`)
   - Domain (`.com` vs `.eu`)

2. It then loads the appropriate pipeline configuration from GitHub:

   - Talent-Shore: Uses the original `pipeline-config.json`
   - FlexSupport: Uses `v2-pipeline-config-org2.json`
   - TeachNow: Uses `v2-pipeline-config-org3.json`
   - Remote Choice: Uses `v2-pipeline-config-org4.json`

3. Each organization has its own cache to prevent conflicts:
   - Talent-Shore: `ragoo_pipeline_config_org1`
   - FlexSupport: `ragoo_pipeline_config_org2`
   - TeachNow: `ragoo_pipeline_config_org3`
   - Remote Choice: `ragoo_pipeline_config_org4`

## File Structure

```
update/
├── js/
│   └── content.js (Updated with multi-org support)
├── pipeline-config.json (Talent-Shore - existing)
├── v2-pipeline-config-org2.json (FlexSupport - existing)
├── v2-pipeline-config-org3.json (TeachNow - existing)
├── v2-pipeline-config-org4.json (Remote Choice - new)
└── README-MULTI-ORG.md (This file)
```

## GitHub Setup

To use this system:

1. Upload all configuration files to your GitHub repository:

   - `pipeline-config.json` (Talent-Shore)
   - `v2-pipeline-config-org2.json` (FlexSupport)
   - `v2-pipeline-config-org3.json` (TeachNow)
   - `v2-pipeline-config-org4.json` (Remote Choice)

2. The extension will automatically fetch the correct configuration based on the current organization context.

## Fallback Behavior

- If an unknown organization is detected, the system defaults to Organization 1's configuration
- All error handling and caching mechanisms remain intact
- The system is backwards compatible with single-organization setups

## Cache Management

Each organization maintains its own cache with a 3-second expiry (as configured). This ensures:

- Fresh data is always fetched when needed
- No cross-organization configuration conflicts
- Optimal performance for each organization context
