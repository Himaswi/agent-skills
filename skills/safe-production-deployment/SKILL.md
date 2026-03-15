---
name: safe-production-deployment
description: >
  Ensures a project is deployed to production safely by checking code quality,
  tests, environment configuration, dependencies, and monitoring setup.
---

## Safe Production Deployment Skill

This skill guides the agent through a safe and structured process for deploying a software project to production while minimizing errors, downtime, and security issues.

---

## When to Use

The agent should use this skill when:

* A project needs to be deployed to a production environment.
* The developer wants to verify that the application is production-ready.
* The system must be checked for configuration, dependency, and security issues before deployment.
* Deployment reliability and system stability are important.

---

## Prerequisites / Inputs

Before executing this skill, the following should be available:

* Access to the project source code repository
* Deployment environment configuration (environment variables)
* Dependency files (e.g., `requirements.txt`, `package.json`)
* Testing framework setup
* Database migration tools (if the project uses a database)

Optional but recommended:

* CI/CD pipeline configuration
* Monitoring and logging tools

---

## Process Steps

The agent should follow these steps in order.

### 1. Verify Code Quality

The agent should review the source code and ensure that:

* No debugging statements such as `console.log()` or unnecessary print statements remain.
* No sensitive information (API keys, passwords, tokens) is hardcoded in the codebase.
* The code follows consistent naming conventions.
* Linting tools report no critical issues.

Example tools:

* ESLint
* Prettier
* Flake8

### 2. Run Application Tests

The agent should verify that the project passes all tests.

Steps:

1. Execute unit tests.
2. Run integration tests if available.
3. Confirm that critical application features work correctly.
4. Verify that edge cases (invalid inputs, empty data, large inputs) are handled properly.

If any tests fail, deployment should be stopped until the issue is fixed.

### 3. Validate Environment Configuration

The agent should confirm that the application is correctly configured for production.

Checks include:

* Environment variables are used instead of hardcoded configuration.
* Correct production values are set for database connections and APIs.
* Separate configuration exists for development and production.

Example environment variables:

* `DATABASE_URL`
* `API_KEY`
* `SECRET_TOKEN`

### 4. Check Dependencies

The agent should confirm that all dependencies are properly installed and secure.

Steps:

1. Verify dependency files are present.
2. Ensure dependency versions are locked.
3. Scan dependencies for known vulnerabilities.

Example tools:

* `npm audit`
* `pip-audit`

### 5. Validate Database Migrations

If the project includes a database, the agent should ensure database safety.

Steps:

1. Confirm database backup exists.
2. Test migration scripts in a staging environment.
3. Avoid destructive changes such as dropping tables without verification.

Migration tools may include:

* Django migrations
* Alembic
* Prisma migrations

### 6. Deploy to Staging Environment

The agent should deploy the application to a staging environment before production.

Deployment flow:

Development → Staging → Production

The staging deployment should verify:

* API functionality
* Authentication systems
* Database operations
* User interface behavior

### 7. Perform Security Checks

Before production deployment, the agent should verify security practices.

Important checks:

* HTTPS is enabled.
* User input validation is implemented.
* Temporary credentials or test accounts are removed.
* APIs require authentication where necessary.

Common risks to prevent:

* SQL Injection
* Cross-Site Scripting (XSS)
* Unauthorized API access

### 8. Deploy to Production

Once all validations pass, the agent may proceed with production deployment.

The deployment should ideally be executed through an automated CI/CD pipeline to reduce manual errors.

Typical pipeline stages:

1. Code validation
2. Test execution
3. Build application
4. Deploy to production

### 9. Monitor the System

After deployment, the agent should monitor the system for issues.

Important metrics include:

* Application errors
* API response time
* Server resource usage

Example monitoring tools:

* Sentry
* Prometheus
* Grafana

### 10. Prepare Rollback Plan

The agent should ensure a rollback strategy exists in case deployment fails.

Rollback procedure:

1. Stop the faulty deployment.
2. Restore the previous stable version.
3. Restore the database backup if necessary.
4. Notify the development team.

This minimizes downtime and protects system stability.

## Output Specification

After executing this skill, the agent should produce:

1. A deployment readiness report summarizing:

   * Code quality status
   * Test results
   * Configuration validation
   * Dependency security status
2. Confirmation that the project is safe for production deployment.
3. A list of any detected issues that must be resolved before deployment.
