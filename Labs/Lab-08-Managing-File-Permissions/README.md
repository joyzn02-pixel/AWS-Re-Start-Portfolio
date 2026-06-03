# Lab 08: Managing File Permissions

## Objectives
- Change folder and file ownership using `chown`
- Modify file permissions using `chmod` (symbolic and absolute modes)
- Assign appropriate permissions to a company folder structure

## Commands Used

### Task 2 – Change Ownership
```bash
sudo chown -R mjackson:Personnel /home/ec2-user/companyA
sudo chown -R ljuan:HR HR
sudo chown -R mmajor:Finance HR/Finance
ls -laR
```

### Task 3 – Change Permission Modes
```bash
sudo chmod g+w symbolic_mode_file
sudo chmod 764 absolute_mode_file
ls -l
```

### Task 4 – Assign Permissions
```bash
sudo chown -R eowusu:Shipping Shipping
sudo chown -R nwolf:Sales Sales
ls -laR Shipping
ls -laR Sales
```

## Key Concepts
| Mode | Example | Meaning |
|------|---------|---------|
| Symbolic | `g+w` | Add write permission for group |
| Absolute | `764` | User=rwx, Group=rw, Others=r |

## AWS Service Used
- **Amazon EC2** – t3.micro instance (Amazon Linux 2)
