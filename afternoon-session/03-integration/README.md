# Accelerator Integration Guide for GR-HEEP

This guide provides step-by-step instructions for integrating an accelerator into the GR-HEEP system.

## Integration Steps

### Step 1: Update Vendor Modules

Run the vendor-update command to integrate the required accelerator modules:

```bash
make vendor-update MODULE=keccak_loosely vendor-update MODULE=keccak_tightly
```

This command fetches and configures both the `keccak_loosely` and `keccak_tightly` modules.

### Step 2: Instantiate Accelerator in Peripherals Template

Instantiate the `keccak_loosely` accelerator in the `gr_heep_peripherals` template:

- Navigate to: `hw/gr-heep/gr_heep_peripherals.sv.tpl`
- Add the accelerator instantiation with appropriate module parameters and signal connections

### Step 3: Connect to Extension Interface

Directly connect the accelerator to the extension interface in the `gr_heep` template:

- Navigate to: `hw/gr-heep/gr_heep.sv.tpl`
- Connect the accelerator signals to the top-level extension interface
- Ensure proper port mappings and signal routing

## Simulation and Testing

Once the accelerator is integrated, follow these steps to simulate and test it:

### Step 1: Generate MCU Configuration

Run the MCU configuration generator:

```bash
make mcu-gen
```

This generates the necessary configuration files and HDL based on your accelerator setup.

### Step 2: Build the Application

Compile the test application:

```bash
make app
```

### Step 3: Build the Verilator Simulation

Build the Verilator simulation:

```bash
make verilator-build
```

### Step 4: Run the Verilator Simulation

Execute the simulation:

```bash
make verilator-run
```

## Testing Applications

The following applications are available for testing the accelerator:

1. **gr_heep_hello_world** (Recommended starting point)
   - Location: `sw/applications/gr_heep_hello_world/`
   - A basic hello world application to verify the accelerator integration

2. **Additional Applications**
   - Locate in: `sw/applications/`
   - Available accelerator-specific test applications:
     - `SHA3-384-baseline`
     - `SHA3-384-loosely`
     - `SHA3-384-tightly`

To test with a specific application, update the build configuration to point to your desired application folder and re-run the build and simulation steps.

## Troubleshooting

- Ensure all vendor modules are properly updated before building
- Verify that the accelerator signals are correctly connected in both templates
- Check simulation logs for any connection or timing issues
- Confirm the MCU configuration is generated after any changes to the accelerator instantiation
