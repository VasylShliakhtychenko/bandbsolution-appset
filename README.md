# Create folder if it doesn't exist
if [ ! -d "../${args.name}" ]; then
mkdir "../${args.name}"
fi

# 1st method to update version(or create if doesn't exist)
echo "app:
  name: ${args.name} 
  version: ${args.version}
values: |
  fullnameOverride: ${args.name}" > config.yaml

# 2nd method to update version
sed -i '' 's/version: .*/version: ${args.version}/' config.yaml

# 3rd method to update version(using yq)
yq e '.app.version = "${args.version}"' config.yaml -i