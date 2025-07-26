
## Testing

### Snapshot Testing
```javascript
const tree = renderer.create(<MyComponent />).toJSON();
expect(tree).toMatchSnapshot();
```

### Mock AsyncStorage
```javascript
jest.mock('@react-native-async-storage/async-storage', () => ({
  setItem: jest.fn(),
  getItem: jest.fn(),
  removeItem: jest.fn(),
}));
```


