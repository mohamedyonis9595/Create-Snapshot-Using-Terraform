# AWS EBS Volume Snapshot via Terraform

This repository contains the Terraform configuration used to automate backup snapshots of existing storage volumes in AWS.

## ⚙️ Specifications
* **Region:** `us-east-1`
* **Target Volume Name:** `nautilus-vol` (5 GB, gp2)
* **Snapshot Name:** `nautilus-vol-ss`
* **Description:** `Nautilus Snapshot`

---

## 💻 Infrastructure Code (`main.tf`)

```hcl
resource "aws_ebs_volume" "k8s_volume" {
  availability_zone = "us-east-1a"
  size              = 5
  type              = "gp2"

  tags = {
    Name        = "nautilus-vol"
  }
}

resource "aws_ebs_snapshot" "nautilus_snapshot" {
  volume_id   = aws_ebs_volume.k8s_volume.id
  description = "Nautilus Snapshot"

  tags = {
    Name = "nautilus-vol-ss"
  }
}
