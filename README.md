```bash
# Store the current version of NPM
NPM_VER=$(npm -v)
LATEST_NPM_VER=$(npm view npm@latest version)
echo "Running with npm@$PREV_NPM_VER"

# Clone this repo
git clone git@github.com:10hendersonm/npm-7-peerdeps-repro.git

# CD down into the example module
cd npm-7-peerdeps-repro/module-a

if [ $NPM_VER != $LATEST_NPM_VER ]; then
  echo "Installing npm@latest"
  npm i -g npm@$LATEST_NPM_VER
  echo ""
else
  echo "npm@latest already installed"
fi

echo "Installing node modules"
# This fails on npm@7.6.0
npm i

if [ $NPM_VER != $LATEST_NPM_VER ]; then
  echo ""
  echo "Re-Installing NPM $NPM_VER"
  npm i -g npm@$NPM_VER
fi
```