from building import *
import os

# Import environment variables
Import('env')

# Get the current working directory
cwd = GetCurrentDir()

# Initialize include paths and source files list
path = [os.path.join(cwd, 'Include')]
src = [os.path.join(cwd, 'Source', 'Templates', 'system_stm32g0xx.c')]

# Map microcontroller units (MCUs) to their corresponding startup files
mcu_startup_files = {
    'STM32G0B0xx': 'startup_stm32g0b0xx.s',
    'STM32G0B1xx': 'startup_stm32g0b1xx.s',
    'STM32G0C1xx': 'startup_stm32g0c1xx.s',
    'STM32G030xx': 'startup_stm32g030xx.s',
    'STM32G031xx': 'startup_stm32g031xx.s',
    'STM32G041xx': 'startup_stm32g041xx.s',
    'STM32G050xx': 'startup_stm32g050xx.s',
    'STM32G051xx': 'startup_stm32g051xx.s',
    'STM32G061xx': 'startup_stm32g061xx.s',
    'STM32G070xx': 'startup_stm32g070xx.s',
    'STM32G071xx': 'startup_stm32g071xx.s',
    'STM32G081xx': 'startup_stm32g081xx.s',
}

# Check each defined MCU, match the platform and append the appropriate startup file
for mcu, startup_file in mcu_startup_files.items():
    if mcu in env.get('CPPDEFINES', []):
        if rtconfig.PLATFORM in ['gcc', 'llvm-arm']:
            src += [os.path.join(cwd, 'Source', 'Templates', 'gcc', startup_file)]
        elif rtconfig.PLATFORM in ['armcc', 'armclang']:
            src += [os.path.join(cwd, 'Source', 'Templates', 'arm', startup_file)]
        elif rtconfig.PLATFORM in ['iccarm']:
            src += [os.path.join(cwd, 'Source', 'Templates', 'iar', startup_file)]
        break

# Define the build group
group = DefineGroup('STM32G0-CMSIS', src, depend=['PKG_USING_STM32G0_CMSIS_DRIVER'], CPPPATH=path)

# Return the build group
Return('group')