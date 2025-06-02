# Vaults.fyi Python SDK

A Python SDK for interacting with the Vaults.fyi API. This package provides feature-equivalent functionality to the JavaScript SDK with Pythonic naming conventions.

## Installation

```bash
pip install vaultsfyi
```

## Quick Start

```python
from vaultsfyi import VaultsSdk

# Initialize the SDK
client = VaultsSdk(api_key="your_api_key_here")

# Get user's idle assets
idle_assets = client.get_idle_assets("0x742d35Cc6543C001")

# Get best deposit options (filtered for USDC/USDS)
deposit_options = client.get_deposit_options(
    "0x742d35Cc6543C001",
    allowed_assets=["USDC", "USDS"]
)

# Get user positions
positions = client.get_positions("0x742d35Cc6543C001")

# Generate deposit transaction
transaction = client.get_actions(
    action="deposit",
    user_address="0x742d35Cc6543C001",
    network="mainnet",
    vault_address="0x...",
    amount="1000000",
    asset_address="0x...",
    simulate=False
)
```

## API Methods

### Vault Methods

#### `get_all_vaults(**kwargs)`
Get information about all available vaults.

```python
vaults = client.get_all_vaults(
    networks=['ethereum', 'polygon'],
    protocols=['aave', 'compound'],
    limit=100
)
```

#### `get_vault(network, vault_address, **kwargs)`
Get detailed information about a specific vault.

```python
vault = client.get_vault(
    network='ethereum',
    vault_address='0x1234...'
)
```

### Historical Data Methods

#### `get_vault_historical_data(network, vault_address, **kwargs)`
Get historical APY and TVL data for a vault.

```python
historical_data = client.get_vault_historical_data(
    network='ethereum',
    vault_address='0x1234...',
    period='30d',
    granularity='daily'
)
```

### Portfolio Methods

#### `get_positions(user_address, **kwargs)`
Get all positions for a user address.

```python
positions = client.get_positions(
    user_address='0x1234...',
    networks=['ethereum', 'polygon']
)
```

#### `get_deposit_options(user_address, allowed_assets=None, **kwargs)`
Get the best deposit options for a user.

```python
options = client.get_deposit_options(
    user_address='0x1234...',
    amount='1000',
    asset='USDC'
)
```

#### `get_idle_assets(user_address, **kwargs)`
Get idle assets in a user's wallet that could be earning yield.

```python
idle_assets = client.get_idle_assets(
    user_address='0x1234...'
)
```

#### `get_vault_total_returns(user_address, network, vault_address, **kwargs)`
Get total returns for a specific user and vault.

```python
returns = client.get_vault_total_returns(
    user_address='0x1234...',
    network='ethereum',
    vault_address='0x5678...'
)
```

#### `get_vault_holder_events(user_address, network, vault_address, **kwargs)`
Get events (deposits, withdrawals) for a specific user and vault.

```python
events = client.get_vault_holder_events(
    user_address='0x1234...',
    network='ethereum',
    vault_address='0x5678...'
)
```

### Transaction Methods

#### `get_transactions_context(user_address, network, vault_address, **kwargs)`
Get transaction context for a specific vault interaction.

```python
context = client.get_transactions_context(
    user_address='0x1234...',
    network='ethereum',
    vault_address='0x5678...'
)
```

#### `get_actions(action, user_address, network, vault_address, **kwargs)`
Get available actions (deposit, withdraw, etc.) for a vault.

```python
actions = client.get_actions(
    action='deposit',
    user_address='0x1234...',
    network='ethereum',
    vault_address='0x5678...',
    amount='1000'
)
```

### Benchmark Methods

#### `get_benchmarks()`
Get benchmark data for comparing vault performance.

```python
benchmarks = client.get_benchmarks()
```



## Error Handling

The SDK provides specific exception types:

```python
from vaultsfyi import VaultsSdk, HttpResponseError, AuthenticationError

try:
    client = VaultsSdk(api_key="invalid_key")
    result = client.get_benchmarks()
except AuthenticationError:
    print("Invalid API key")
except HttpResponseError as e:
    print(f"API error: {e}")
```

## Requirements

- Python 3.8+
- requests


## License

MIT License

## Author

Kaimi Seeker (kaimi@wallfacer.io)