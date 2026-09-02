🚀 Day 71 – CI/CD Fundamentals
🎯 Objective
Understand the fundamentals of CI/CD, why automation is important in DevOps, and how source code moves from a developer's commit to a deployed application.
🔄 What is CI/CD?
CI/CD is a set of practices and automation techniques used to continuously integrate, test, deliver, and deploy software.
The basic idea is:
Code
  ↓
Build
  ↓
Test
  ↓
Package
  ↓
Deploy
  ↓
Release
  ↓
Monitor
The goal is to deliver software faster, more reliably, and with fewer manual errors.
🔵 Continuous Integration (CI)
Continuous Integration is the practice of frequently integrating code changes into a shared repository and automatically validating those changes.
Developer
    ↓
Git Commit
    ↓
GitHub
    ↓
CI Pipeline
    ↓
Build
    ↓
Automated Tests
    ↓
Feedback
CI focuses on:
Frequent code integration
Automated builds
Automated testing
Early bug detection
Fast developer feedback
🟢 Continuous Delivery
Continuous Delivery automatically builds, tests, and prepares software so that it is always ready for release.
A production release may still require manual approval.
Code
 ↓
Build
 ↓
Test
 ↓
Package
 ↓
Staging
 ↓
Manual Approval
 ↓
Production
🟠 Continuous Deployment
Continuous Deployment goes one step further.
Validated changes are automatically deployed to production without a manual approval step.
Code
 ↓
Build
 ↓
Test
 ↓
Package
 ↓
Deploy
 ↓
Production
