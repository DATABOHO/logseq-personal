- ✅ Recommended: Auto-Start Tailscale on Boot
- To avoid this problem in the future, enable Tailscale auto-start:
- On Windows:
  1.	Open PowerShell as Admin.
  2.	Run:
- ```powershell
  / Set-Service -Name TailscaleService -StartupType Automatic
  ```
-