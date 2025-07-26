
## React Native

### Threading
- JS thread: Runs app logic
- Shadow thread: Handles layout
- Main/UI thread: Handles rendering

### Features
- Bridging: Connects JS to native modules via async communication
- JSI: New way to interact with native modules using C++
- FlatList: High-performance list view for large data sets

### FlatList Optimization
- `keyExtractor`: Identify list items uniquely
- `initialNumToRender`: Reduce first render time
- `maxToRenderPerBatch`: Control render rate
- `windowSize`: Optimize memory usage
- `removeClippedSubviews`: Free up memory
- `getItemLayout`: Improve scroll for fixed height items
- `React.memo`: Prevent unnecessary re-renders
- `useCallback`: Avoid recreating render functions

### Development Tools
- Optimization: Lazy loading, avoiding unnecessary re-renders
- Debugging: Flipper, Chrome Debugger, React DevTools
- React Navigation: Handles navigation stacks, tabs, transitions
- Security: Protect app data, code, and API endpoints
