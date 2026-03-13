# ==========================================
# Starknet Contracts Builder
# ==========================================
FROM softwaremansion/scarb:latest

# Set working directory
WORKDIR /app

# Copy configuration files
COPY Scarb.toml ./

# Copy source code
COPY . .

# Build the contracts (This generates the Sierra/Casm files in the target folder)
RUN scarb build

# Default command: show build result
CMD ["scarb", "build"]
