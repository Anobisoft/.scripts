"# Skill: Proper Use of edit_existing_file and single_find_and_replace Commands

## Problem Encountered
When trying to update file, I struggled with:
1. Escaping quotes properly in complex strings
2. Handling multi-line replacements correctly
3. Getting the right format for command execution

## Solution Approach

### For edit_existing_file:
- Use simple text replacement when possible
- Avoid complex escaping of quotes
- Make sure the new content is clearly distinguishable from old content
- Test with small changes first

### For single_find_and_replace:
- Use exact string matching for both old and new content
- Be careful about line endings and whitespace
- Ensure the replacement text is exactly what you want to see in file
- The command works best with clear, distinct content blocks

## Best Practices
1. Always read the file first to understand its current state
2. Make minimal changes - only add documentation, don't change commands
3. Use single_find_and_replace for exact pattern replacements
4. Avoid complex escaping when possible - simpler is better
5. Test changes by reading file after operation

## Key Takeaway
When dealing with configuration files that need comment additions:
1. Read current file content
2. Prepare new content with clear comments
3. Use single_find_and_replace for exact replacements
4. Don't overthink the escaping - keep it simple"
