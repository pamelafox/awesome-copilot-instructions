# Copilot Instructions

This document provides comprehensive guidelines for generating code using GitHub Copilot in our project. The instructions combine best practices with our specific requirements and default tech stack.

## Objectives
- Generate clear, maintainable, and testing-friendly code.
- Ensure the code includes thorough documentation and data type declarations.
- Encourage the use of primary logging for printing events.
- Produce comprehensive tests with new classes.

## Guidelines

### 1. Documentation and Comments
- Every class and method must have comments explaining their purpose and functionality.
- Example:
  ```python
  # A class representing a data processor.
  class DataProcessor:
      # Initializes the DataProcessor with initial configuration.
      def __init__(self, config: dict) -> None:
          """
          Initialize with configuration settings.
          
          :param config: Dictionary containing configuration parameters.
          """
          self.config = config
  ```

### 2. Data Type Declarations
- Methods and functions must declare the data types for both parameters and return values.
- Example:
  ```python
  def add_numbers(a: int, b: int) -> int:
      """
      Adds two integers and returns the sum.
      
      :param a: First integer.
      :param b: Second integer.
      :return: The sum of a and b.
      """
      return a + b
  ```
#### - Metrics class inheritance of Metric class
- All new metrics should inherit from the base Metric class.
- Ensure that the new metrics class implements all required methods and properties.
- Example:
  ```python
  class CustomMetric(Metric):
      def calculate(self) -> float:
          # Custom calculation logic
          pass
  ```


### 3. Testing Friendly Code
- Code should be written in a manner that facilitates unit testing.
- Separate business logic from UI and external dependencies.
- Use dependency injection where possible to make testing easier.

### 4. Test Creation with New Classes
- Create separate test classes for new code. These tests should cover different scenarios and edge cases.
- Place tests in designated test files or directories.
- Example (using Python's unittest):
  ```python
  import unittest
  from my_module import DataProcessor
  
  class TestDataProcessor(unittest.TestCase):
      def test_initialization(self):
          config = {"key": "value"}
          processor = DataProcessor(config)
          self.assertEqual(processor.config, config)
  
  if __name__ == '__main__':
      unittest.main()
  ```

### 5. Primary Logging for Printing Events
- Use the primary logging mechanism for printing events instead of using print statements directly.
- Example:
  ```python
  import logging
  
  # Configure primary logger
  logging.basicConfig(level=logging.INFO)
  logger = logging.getLogger(__name__)
  ```

### 6. Data Structure Conventions
- Example:
  ```python
  @dataclass(slot=True)
  class ProfitMetrics:
      __slots__ = (xxxx)

      __init__(self, profit: float, loss: float) -> None:
          """
          Initialize profit metrics.
          
          :param profit: Total profit amount.
          :param loss: Total loss amount.
          """
          self.profit = profit
          self.loss = loss

          # Implementation follows...


      async def store_profit_data(self, profit_data: dict) -> None:
          """
          Store profit data in Redis.
          
          Uses hash map for current stats and sorted set for historical data.
          All keys have 30-day TTL.
          
          :param profit_data: Dictionary containing profit metrics
          """
          # Implementation follows...
  ```

### 7. Asynchronous Programming
- Use async/await consistently throughout the codebase
- Implement proper exception handling in all async functions
- Use async locks when modifying shared data structures
- Follow the existing pattern of using asyncio.create_task for non-blocking operations
- Example:
  ```python
  import asyncio
  
  async def process_market_data(self, market_data: dict) -> None:
      """
      Process market data asynchronously.
      
      :param market_data: Dictionary containing market data
      """
      try:
          async with self.lock:
              # Process data safely
              await self.store_metrics(market_data)
      except Exception as e:
          logger.error(f"Error processing market data: {e}")
          # Record error metric
  ```

### 8. "Project specfic" Implementation
- Extend the base Metric class for new metric types
- Implement Chart.js compatible output methods
- Store raw metrics data and derived statistics separately
- Follow the established pattern for time-series data
- Include methods for both real-time and historical analytics

### 9. Performance Optimization for Low Latency
- **CRITICAL**: All code must be optimized for low latency environments where microseconds matter
- Implement efficient algorithms with O(1) or O(log n) time complexity where possible
- Minimize memory allocations and garbage collection triggers
  - Use object pooling for frequently created/destroyed objects
  - Pre-allocate buffers and arrays where sizes are predictable
- Avoid blocking operations in the main execution path
  - Use non-blocking I/O operations
  - Implement circuit breakers for external service calls
- Optimize data structures for quick access patterns
  - Use fixed-size arrays instead of dynamic collections where appropriate
  - Consider memory layout and cache locality for hot path data
- Profile critical code paths regularly
  - Identify and eliminate bottlenecks
  - Benchmark against defined latency SLAs
- Minimize external dependencies that could introduce latency
- Use lock-free algorithms and data structures when possible
- Example:
  ```python
  class OrderBookCache:
      def __init__(self, symbols: list[str]) -> None:
          """
          Pre-allocate order book caches for fast access.
          
          :param symbols: List of trading symbols to monitor
          """
          # Pre-allocate fixed data structures
          self.books = {symbol: self._create_empty_book() for symbol in symbols}
          # Use numpy arrays for numeric calculations
          self._price_levels = np.zeros(10, dtype=np.float64)
          
      def update_book(self, symbol: str, data: dict) -> None:
          """
          Update order book with minimal allocations.
          
          :param symbol: Trading symbol
          :param data: Order book update data
          """
          book = self.books.get(symbol)
          if not book:
              return  # Early return to avoid unnecessary processing
              
          # Zero-copy or minimal copy operations
          # ...
  ```

## Default Tech Stack
- **Python**: Used for backend logic and scripting.
- **Chart.js**: For data visualization.
- **Redis**: For metrics storage and caching.
- **Asyncio**: For asynchronous programming patterns.

## Coding Style and Best Practices
- **Modularity**: Write modular code that is easier to maintain and test.
- **Consistency**: Follow consistent naming conventions and coding standards.
- **Error Handling**: Incorporate robust error and exception handling mechanisms.
- **Comments**: Ensure every class, method, and critical section of code has explanatory comments.
- **ES6 Syntax for Frontend**: For jQuery/Bootstrap/Chart.js parts, ensure modern ES6+ practices if using JavaScript.

## Conclusion
These instructions are designed to ensure that GitHub Copilot produces code that is efficient, well-documented, adaptable for testing, and adheres to our project requirements. Feel free to iterate on these guidelines as the project evolves.