
```yaml
- --enable-admission-plugins=ImagePolicyWebhook
- --admission-control-config-file=/etc/image-policy/image-policy-config.yaml
```

#### Volume Mounts:

```yaml
volumeMounts:
  - name: image-policy-config
    mountPath: /etc/kubernetes/image-policy
    readOnly: true
```

#### Volumes:

```yaml
volumes:
  - name: image-policy-config
    hostPath:
      path: /etc/kubernetes/image-policy
      type: DirectoryOrCreate
```

---

### 2️⃣ Confirm contents of `image-policy-config.yaml`

```yaml
apiVersion: apiserver.config.k8s.io/v1
kind: AdmissionConfiguration
plugins:
  - name: ImagePolicyWebhook
    path: /etc/image-policy/image-policy-webhook-config.yaml
```

---

### 3️⃣ Confirm contents of `image-policy-webhook-config.yaml`

```yaml
imagePolicy:
  kubeConfigFile: /etc/kubernetes/image-policy/webhook-kubeconfig.yaml
  allowTTL: 50
  denyTTL: 50
  retryBackoff: 500
  defaultAllow: false
```

---

