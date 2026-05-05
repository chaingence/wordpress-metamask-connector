# Supply Chain Security Checklist

## ⚠️ Critical: Package Manipulation Prevention

This checklist helps prevent supply chain attacks like the SAP/npm compromise and similar incidents.

---

## npm/JavaScript Package Security

### Before Installing Packages
- [ ] **Audit packages first**: Run `npm audit` or `yarn audit` before install
- [ ] **Check package reputation**: Use Socket.dev or Snyk to scan packages
- [ ] **Verify package.json scripts**: NEVER blindly run preinstall/postinstall hooks
- [ ] **Review package contents**: Check `node_modules` before adding to project
- [ ] **Use lockfiles**: Commit `package-lock.json` / `yarn.lock` to detect tampering

### Package Installation Rules
- [ ] **Never auto-trust**: `npm install` should require explicit review
- [ ] **Isolate in CI/CD**: Never run `npm install` with production credentials
- [ ] **Private registry**: Use Verdaccio or similar for internal packages
- [ ] **Version pinning**: Lock to exact versions, not ranges
- [ ] **Hash verification**: Use Subresource Integrity when available

### Credentials & Tokens
- [ ] **Least privilege**: npm/GitHub tokens with minimal required permissions
- [ ] **Rotate regularly**: API keys, SSH keys, tokens on a schedule
- [ ] **Never in builds**: Build processes should NOT have production credentials
- [ ] **Separate CI credentials**: Use dedicated service accounts for CI/CD

---

## General Supply Chain Security

### Code Integrity
- [ ] **Verify sources**: Only use official registries and verified sources
- [ ] **Check signatures**: If available, verify package signatures
- [ ] **Monitor for anomalies**: Set up alerts for unusual package behavior

### Infrastructure Protection
- [ ] **Separate backups**: Never store backups in same volume as production
- [ ] **Kubernetes secrets**: Use proper secret management (not in config files)
- [ ] **Cloud IAM**: Apply least-privilege principles for all cloud access

### Monitoring & Response
- [ ] **Enable audit logs**: CloudTrail, GCP Activity, Kubernetes Audit Logs
- [ ] **Set up alerts**: Monitor for unauthorized access attempts
- [ ] **Incident response plan**: Have a playbook for supply chain incidents

---

## If Compromised: Immediate Actions

1. **Revoke all credentials** that were exposed
2. **Audit installed packages** for unexpected changes
3. **Rotate ALL secrets**: SSH keys, API keys, tokens, Cloud credentials
4. **Check for new GitHub accounts** created by attackers
5. **Reinstall from lockfile**: `rm -rf node_modules && npm ci`
6. **Report incident**: To package registry and security community

---

## References

- SAP Supply Chain Attack: https://socket.dev/blog/sap-cap-npm-packages-supply-chain-attack
- SAP Security Note: https://me.sap.com/notes/3747787
- Socket.dev: https://socket.dev
- npm Security Best Practices: https://docs.npmjs.com/

---

*Last updated: 2026-05-05*
*This document is maintained by the security team. Update when new threats emerge.*