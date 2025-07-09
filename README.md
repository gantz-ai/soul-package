# Soul Package Manager

A categorized package repository for the Soul programming language with version management support.

## Structure

```
soul-package/
├── io/              # Input/Output operations
├── network/         # Network communication
├── data/           # Data processing
├── utility/        # Utility functions
└── index.json      # Package registry
```

## Categories

### 📁 **io** - Input/Output Operations
- **console** - Console operations with color and formatting support
- **file** - File system operations

### 🌐 **network** - Network Operations  
- **http** - HTTP client and server utilities

### 📊 **data** - Data Processing
- **json** - JSON parsing and serialization

### 🔧 **utility** - Utility Functions
- **math** - Mathematical operations
- **time** - Time and date handling

## Package Versioning

Each package supports multiple versions:
```
package-name/
├── 1.0.0/
│   ├── index.soul
│   └── soul.json
├── 2.0.0/
│   ├── index.soul
│   └── soul.json
└── README.md
```

## Usage

### Finding Packages
```bash
# Search by category
grep -r "io" index.json

# Find latest version
jq '.packages.console.latest' index.json

# Get package path
jq '.packages.console.versions."2.0.0".path' index.json
```

### Installing Packages
```soul
// Import specific version
import Console from "io/console/2.0.0"

// Import latest (resolved via package manager)
import Console from "console@latest"
```

## Package Structure

Each package version contains:
- `index.soul` - Main package file
- `soul.json` - Package metadata and dependencies
- `README.md` - Package documentation (optional)

## Adding New Packages

1. Create category folder if needed
2. Create package folder with version
3. Add `index.soul` and `soul.json`
4. Update `index.json` registry
5. Add documentation

## Registry Format

The `index.json` file contains:
- **categories** - Category definitions and paths
- **packages** - Package metadata with version history
- **latest** - Latest version tracking
- **changelog** - Version update notes

## Contributing

1. Follow semantic versioning (semver)
2. Maintain backward compatibility when possible
3. Update changelog for new versions
4. Add tests for new functionality
5. Update documentation

## License

MIT License - See individual package licenses for details.