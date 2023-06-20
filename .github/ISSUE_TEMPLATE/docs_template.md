---
name: Documentation request
about: Suggest a documentation change to Redpanda
---

body:
  - type: input
    id: issue-description
    attributes:
      label: Describe the issue
      description: What problem does this issue solve for customers?
Who is the audience for this update? For example, cluster admins, or developers?
Do you know the context in which users will likely search for this content? If so, share it.
If this is a new feature, add a label for the version in which the update is expected.
    validations:
      required: true


update:
  - type: input
    id: update-doc
    attributes:
      label: Sample Input
      description: Provide the URL of the page(s) to which the updates apply.
Which topic(s) should be updated?
What is the requested fix? Describe what is wrong in the existing doc and include screenshots if possible. Then provide the correct information.
Is this request to document an existing Redpanda feature that is not currently documented?
    validations:
      required: false