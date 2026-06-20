Day 3 - 6/20/26 2:40pm Issue #4
* Problem: Client VM boots to a black screen inside VB (VirtualBox), the VM status says "Running."
* Hypothesis: Gemini says likely cause is Hyper-V conflict - Windows's virtualization features use the same VT-x/AMD-V hardware that VB needs. This leads to a "nested virtualization." The Win Server VM works fine as it does not enforce/enable requirements of Win 11: TPM 2.0 and Secure Boot. When VB refuses to boot the Win 11 VM, it is because it does not detect these security requirements. Since the other VM is working fine, the problem is likely with the requirements of the specific VM of Win 11 and not with any host virtualization infrastructure.
* Test of Hypothesis: Enable "EFI(special OSes only)" in VB settings - couldn't find that option, but moved on and verified VM had the following settings:
  - 2 processors [X]
  - TPM v2.0 [x]
  - Secure Boot enabled [ x ]
  - > Screen settings - changed Graphics Controller VBoxVGA > VMSVGA
  - 3D Acceleration disabled [x]

Tried to boot again

Eureka! It worked. 🥳

* Solution: Apparently changing graphics controller in the screen settings from VBoxVGA to VMSVGA was enough. 


* Lessons Learned: Ask Gemini and you may have your problem fixed in a few minutes (30 minutes with documentation time)
