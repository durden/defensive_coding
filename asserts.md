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

# Executable documentation

- doctests++
- Runs alongside production code
- Enabled by default

--------------------------------------------------

# Close to source

- Debugging is hard
- Close gap between symptom and cause
- Alert return conditions

--------------------------------------------------

# Invalid parameters

- Write good messages
- Avoid unreproducible bugs
- New use cases
- Invalid assumptions about environment
- Documentation oversights

--------------------------------------------------

# Assert downsides

- Debug mode
- Increased noise

--------------------------------------------------

# Avoid this

    !python
    def normalize_ranges(button_state):
        assert isinstance(button_state['colname'], str)
        assert button_state['datamin'] >= 0
        assert button_state['datamax'] >= 0
        assert button_state['datamin'] <= button_state['datamax']

        # 1-D numpy array of data
        live_data = get_column_data(button_state['colname'])
        assert len(live_data), 'Empty live data'

        colspan = numpy.max(live_data) - numpy.min(live_data)
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
