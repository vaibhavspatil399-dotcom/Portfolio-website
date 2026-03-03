import os

# Create output directory
os.makedirs("output", exist_ok=True)

# -------------------------
# Collect user information
# -------------------------
print("\n=== Portfolio Website Generator ===\n")

name = input("Enter your full name: ")
bio = input("Write a short bio about yourself: ")
skills = input("Enter your skills (comma-separated): ")
projects = input("Enter your projects (comma-separated): ")
email = input("Enter your contact email: ")
linkedin = input("Enter your LinkedIn URL: ")
github = input("Enter your GitHub URL: ")

# Convert comma input to list
skills_list = [s.strip() for s in skills.split(",")]
projects_list = [p.strip() for p in projects.split(",")]

# -------------------------
# Read HTML template
# -------------------------
with open("template.html", "r") as file:
    template = file.read()

# Replace placeholders
html_output = template.replace("{{NAME}}", name)\
                      .replace("{{BIO}}", bio)\
                      .replace("{{EMAIL}}", email)\
                      .replace("{{LINKEDIN}}", linkedin)\
                      .replace("{{GITHUB}}", github)\
                      .replace("{{SKILLS}}", "".join(f"<li>{s}</li>" for s in skills_list))\
                      .replace("{{PROJECTS}}", "".join(f"<li>{p}</li>" for p in projects_list))

# -------------------------
# Save generated HTML
# -------------------------
with open("output/index.html", "w") as file:
    file.write(html_output)

print("\n Portfolio website generated successfully!")
print(" Open: output/index.html in your browser.\n")
