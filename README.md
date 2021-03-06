# Azure Gaming 
## About
The setup script configures everything that's needed to run or develop games via Remote Desktop. It use Azure NV6 virtual machine (VM) with a single Nvidia M60 GPU (1/2 of a M60 graphics card).

These scripts Deploy Azure VMs Optimised for Gaming. It is based on https://github.com/ecalder6/azure-gaming and removed some functionality like Zero VPN, Steam and added Azure Hybrid Benefit for Windows Server and Low Piority VM without Lose Data.

Orginal project was inspired by this (https://lg.io/2016/10/12/cloudy-gamer-playing-overwatch-on-azures-new-monster-gpu-instances.html).


## Disclaimer
**This software comes with no warranty of any kind**.

## Pricing
To game on the cloud on Azure, you will have to pay for the virtual machine, outgoing data bandwidth from the VM, and managed disk space. 

You can pick between 2 kinds of VM: standard and low priority. A low priority VM is around **60%** cheaper than a standard VM. 
Low Piority VM can stop anytime, but you do not lose your data. You can also use Azure Hybrid Benefit for Windows Server.

The calculators below are prepopulated with an estimated monthly price for playing 35 hours a month in West US 2 region. It assumes that you stream at an averge of around 30 Mbits/second (13.5 GBs an hour) and use one 128GB managed disk. You can divide the total by 35 to find the estimated cost per hour.

Azure also charges you for the number of transactions on managed disk. The calculator assumes 100k transactions a month (no idea how accurate this is).

* [Price Calculator for Standard](https://azure.com/e/5479babbd37e46b68730b27e9fd1a641)
* [Price Calculator for Low Priority](https://azure.com/e/f0e1298bc0984f178ba002d3316d9974)


## Usage
Just push the button Deploy To Azure.
If you Open Device Manager and you can not see NVIDIA Tesla M60 Graphics Card just open PowerShell and type:

Start-Process -FilePath "C:\NVIDIA\DisplayDriver\391.03\Win10_64\International\setup.exe" -ArgumentList "-s", "-noreboot" -Wait

After that please restart computer and open PowerShell in Admin mode agian and issue:

$nvsmi = "C:\Program Files\NVIDIA Corporation\NVSMI\nvidia-smi.exe"
$gpu = & $nvsmi --format=csv,noheader --query-gpu=pci.bus_id
& $nvsmi -g $gpu -fdm 0

and restart computer just again.

### II. Automatically Deploy Your Azure VM
#### Automated Standard
<a href="https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FMariuszFerdyn%2Fazure-gaming%2Fmaster%2FStandard.json" target="_blank">
    <img src="http://azuredeploy.net/deploybutton.png"/>
</a>

#### Automated Low Priority
<a href="https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FMariuszFerdyn%2Fazure-gaming%2Fmaster%2FLowPri.json" target="_blank">
    <img src="http://azuredeploy.net/deploybutton.png"/>
</a>
