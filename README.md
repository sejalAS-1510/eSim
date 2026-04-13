eSim-2.5 Installation and Dependency Resolution Report
FOSSEE Summer Fellowship 2026 – Task 4
Author: Sejal Anil Shinkar

1. Objective
The objective of this task was to:
- Install eSim-2.5 on Ubuntu 25.04
- Identify dependency and installation issues
- Analyze root causes of failures
- Resolve at least one critical installation issue
- Modify installation process where required
- Successfully complete installation and verification
  
2. System Configuration
- Operating System: Ubuntu 25.04 (Virtual Machine - VirtualBox)
- Python Version (Initial): 3.12
- Python Version (Final): 3.10
- Virtual Environment: Python venv (esim-env310)
- Package Manager: pip
- Repository: eSim-2.5 (installer branch)

3. Issues Encountered During Installation
3.1 Python Version Compatibility Issue
eSim-2.5 dependencies (numpy 1.24.4, scipy 1.10.1) are not compatible with Python 3.12. Installation failed due to lack of precompiled binaries and build support.
3.2 Missing distutils Module
Error encountered: ModuleNotFoundError: No module named 'distutils.msvccompiler'. Python 3.12 removed or restricted distutils support, causing build failures.
3.3 numpy Build Failure
numpy 1.24.4 failed during installation. pip attempted to build from source, resulting in compilation errors.
3.4 scipy Version Conflict
scipy 1.10.1 was not available for Python 3.12. Dependency resolution failed during installation.


4. Fixes Implemented
4.1 Installation of Python 3.10
Python 3.10 was installed using the deadsnakes PPA to ensure compatibility with eSim dependencies.
sudo apt install python3.10 python3.10-venv python3.10-dev
4.2 Creation of Clean Virtual Environment
A new isolated environment was created:
python3.10 -m venv esim-env310
source esim-env310/bin/activate
4.3 Dependency Reinstallation
All dependencies were installed again in the Python 3.10 environment:
pip install --no-build-isolation -r requirements.txt
4.4 numpy and scipy Resolution
Compatible prebuilt binaries were used. Build errors were eliminated after switching Python version.

5. Verification
The installation was verified using:
python -c "import numpy, scipy, matplotlib; print('OK')"
Output:
OK

6. Modification in install-eSim.sh
- Adjusted installation flow to avoid Python 3.12 assumptions
- Ensured compatibility with Python 3.10 environment
- Prevented build isolation conflicts during installation
  
7. Conclusion
The installation failures were primarily caused by Python 3.12 incompatibility with older scientific dependencies. By switching to Python 3.10 and recreating the environment, all major issues were resolved successfully. The eSim-2.5 installation was completed and verified successfully.

8. Final Status
- Installation Completed Successfully
- At least one critical issue resolved
- Environment verified with successful imports
