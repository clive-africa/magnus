# sentinel - SAM Capital Calculation Tool

## Overview

Sentinel is a comprehensive Excel-based tool designed to streamline Solvency Assessment and Management (SAM) capital calculations for South African short-term insurers. Currently implemented as an Excel workbook with VBA modules, Sentinel will be published as an Excel Add-in to provide seamless integration with existing actuarial workflows.

## Purpose

For far too long the SOuth African non-life industry, actuarial profesisonals and many insurance companies have "made do" with processes and tools that are not appropriate for the regular calcualtion of SAM capital requirements. We require proper tools to calculate regulatory capital under the SAM framework. Sentinel aims to partly addresses this need by providing:

- **Automated Capital Calculations**: Non-life capital requirement calcualtions including premiuma and reserve risk, natural catastrophe risk, factor based and non-proprotional capitla requirements
- **Multi-dimensional Analysis**: Support for complex organizational structures and reinsurance arrangements
- **Regulatory Compliance**: Built specifically for SAM requirements applicable to South African insurers
- **Efficiency**: Replaces manual calculation workbooks with automated, auditable functions

## Key Features

### Current Functionality

#### 🌊 Scenario Based Natural Catastrophe Capital (Nat Cat)
- Calculates scenario based natural catastrophe capital requirements for natural perils (earthquake, hail, horizontal.)
- Applies regulatory based calculations
- Caters for mapping of postal codes as per regulatory requirements

#### 🌊 Factor Based Natural Catastrophe Capital (Factor Nat Cat)
- Calculates factor based capital requirements for natural perils (earthquake, flood, storm, etc.)
- Applies regulatory factor-based approach
- Handles 19 distinct natural catastrophe perils
- Automatic LOB exclusions per regulatory requirements

#### 📊 Non-Proportional Catastrophe Capital (Factor NP Cat)
- Specialized calculations for non-proportional treaties
- Excess of loss cover analysis
- Supports 3 aggregate peril categories
- LOB-specific inclusion rules

#### 🔄 Reinsurance Integration
- Net capital calculation after reinsurance recoveries
- Multi-layer treaty handling
- Counterparty allocation and tracking
- Pro-rata recovery distribution

#### 🏢 Organizational Structure Support
- Multiple organizational levels (company, division, branch, etc.)
- Flexible aggregation across any number of levels
- Maintains consistency across all aggregation points

### Technical Capabilities
sentinel uses efficient tensore operations for mult-dimensional calculations. This allows for the calcualtion of 


## Installation

### Current Version (Excel Workbook)

1. Download the latest release from the [Releases](https://github.com/clive-africa/sentinel/releases) page
2. Open the Excel file in Microsoft Excel (2016 or later recommended)
3. Enable macros when prompted

### Requirements

- Microsoft Excel 2016 or later
- Windows operating system (recommended)
- Macros must be enabled

## Usage

### Basic Workflow

1. **Data Preparation**
   - Prepare your premium and reserve data according to the template format
   - Ensure all required columns are present (see Data Format section)
   - Set inclusion flags for factor-based calculations

2. **Configuration**
   - Select calculation type (Natural Cat or Non-Proportional)
   - Specify organizational levels to analyze
   - Configure reinsurance structures (optional)

3. **Execution**
   ```vba
   ' Example: Calculate Natural Catastrophe capital with 2 organizational levels
   =FactorNatCat(PremiumData, 2)
   
   ' Example: Include reinsurance calculations
   =FactorNatCat(PremiumData, 2, Contracts, Counterparties, Programmes)
   ```

4. **Results**
   - Review capital charges by level, peril, and structure
   - Analyze gross vs. net positions
   - Export results for reporting

### Data Format

Your input data should include the following columns:

| Column | Description | Required |
|--------|-------------|----------|
| level_1 | Primary organizational level | Yes |
| level_2 | Secondary organizational level | Optional |
| lob_type | Line of business type (P/NP/FP/FNP/O/FO) | Yes |
| lob | Specific LOB code (1a, 2b, etc.) | Yes |
| gross_p | Current period gross premium | Yes |
| gross_p_last | Prior period gross premium | Optional |
| ri_structure | Reinsurance structure identifier | Optional |
| include_factor_cat | Include in Nat Cat calculation (Y/N) | Yes |
| include_np_cat | Include in NP Cat calculation (Y/N) | Yes |

## Module Structure

```
Sentinel/
├── mFactorCat.bas          # Main calculation engine
├── mHelpers.bas            # Utility functions
├── mSetup.bas              # Configuration and metadata
├── mReinsurance.bas        # Reinsurance calculations
├── clsEvent.cls            # Event class for catastrophe modeling
├── clsCounterparty.cls     # Counterparty management
└── cPos.cls                # Position tracking utilities
```

## LOB Mappings and Rules

### Natural Catastrophe Exclusions
The following LOBs are automatically excluded from Nat Cat calculations:
- 3i (Credit)
- 9 (Guarantee)
- 15 (Miscellaneous)
- 17i-17iv (Legal expenses variants)

### Natural Catastrophe Mappings
- Non-Proportional (NP) → 18b (except marine)
- Facultative Non-Prop (FNP) → 18e (except marine)
- Other (O) → 18c
- Facultative Other (FO) → 18f

## Development Roadmap

### Phase 1: Current (Excel Workbook) ✅
- Core calculation engine
- Basic UI in Excel
- Manual data input

### Phase 2: Add-in Conversion (In Progress)
- Convert to .xlam add-in format
- Ribbon interface integration
- Custom task panes

### Phase 3: Enhanced Features (Planned)
- Database connectivity
- Automated report generation
- Scenario analysis tools
- Sensitivity testing

### Phase 4: Advanced Analytics (Future)
- Machine learning integration
- Predictive modeling
- Real-time monitoring dashboard

## Contributing

We welcome contributions from the actuarial and insurance community! Please see our [Contributing Guidelines](CONTRIBUTING.md) for more information.

### Areas for Contribution
- Additional catastrophe perils
- International regulatory frameworks
- Performance optimizations
- Documentation improvements
- Test cases and validation

## Testing

Run the test suite using the included test workbook:
```
Sentinel_Tests.xlsm
```

Test coverage includes:
- Unit tests for individual functions
- Integration tests for complete workflows
- Validation against regulatory examples

## Support

For support, please:
1. Check the [Documentation](docs/) folder
2. Review [Frequently Asked Questions](FAQ.md)
3. Open an issue on [GitHub](https://github.com/clive-africa/sentinel/issues)
4. Contact the development team

## License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

## Regulatory Compliance

Sentinel is designed to comply with:
- South African Solvency Assessment and Management (SAM) framework
- Prudential Authority requirements

**Disclaimer**: While Sentinel is designed to assist with regulatory calculations, users remain responsible for ensuring compliance with all applicable regulations. Always validate results and consult with qualified actuaries.

## Version History

| Version | Date | Description |
|---------|------|-------------|
| 0.0.1 | Nov 2025 | Initial release with core Nat Cat and NP Cat calculations |


## Contact

**Author**: Clive Hogarth  
**Repository**: [https://github.com/clive-africa/sentinel](https://github.com/clive-africa/sentinel)

---
