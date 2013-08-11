# Asserts

- Not just for unit tests
- Check assumption, raise AssertionError

--------------------------------------------------

# Asserts

    !python
    def normalize_ranges(button_state):
        # 1-D numpy array of data
        live_data = get_column_data(button_state['colname'])
        colspan = numpy.max(live_data) - numpy.min(live_data)

        ratio = {}
        ratio['min'] = button_state['datamin'] / colspan
        ratio['max'] = button_state['datamax'] / colspan
        assert 0.0 <= ratio['min'] <= 1.0, (
                '"%s" min (%f) not in [0-1] given (%f)')
        assert 0.0 <= ratio['max'] <= 1.0, (
                '"%s" max (%f) not in [0-1] given (%f)')
        return ratio

--------------------------------------------------

# Assert benefits

- Clear intent/docs
- Complain early and often
- Debug info when it counts

--------------------------------------------------

# Clear intent

- doctests++
- Runs alongside production code
- Enabled by default
- Executable documentation

--------------------------------------------------

# Complain early, often

- Debugging is hard
- Close gap between symptom and cause
- Alert return conditions

--------------------------------------------------

# Debug info when it counts

- Good messages include parameters and local state
- Invalid assumptions about environment
- Avoid unreproducible bugs

## More information leads to:

- New use cases
- Documentation oversights

--------------------------------------------------

# Assert downsides

- Only available in debug mode
- Increased code noise

# Presenter Notes

- Use -O to run in optimized mode, turns off asserts for performance
- Default is debug on
- Docs say it's clear to use for debug, not production

--------------------------------------------------

# Avoid this
.fx: small

    !python
    def normalize_ranges(button_state):
        assert isinstance(button_state['colname'], str)
        assert button_state['datamin'] >= 0
        assert button_state['datamax'] >= 0
        assert button_state['datamin'] <= button_state['datamax']

        live_data = get_column_data(button_state['colname'])
        colspan = numpy.max(live_data) - numpy.min(live_data)

        assert len(live_data), 'Empty live data'
        assert colspan >= 0, 'Colspan (%f) is negative' % (colspan)

        ratio = {}
        ratio['min'] = button_state['datamin'] / colspan
        ratio['max'] = button_state['datamax'] / colspan

        assert 0.0 <= ratio['min'] <= 1.0
        assert 0.0 <= ratio['max'] <= 1.0
        return ratio

--------------------------------------------------

# Good assert usage

- Check return values, not inputs
- Document usage in style guide
- Don't ruin duck-typing

# Presenter Notes
- Checking returns can allow you to complain about inputs if you get wrong
  answer, so it's a 2 for 1
