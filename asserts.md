# Asserts

- Not just for unit tests
- Check assumption, raise AssertionError

--------------------------------------------------

# Find the assumptions

    !python
    def normalize_ranges(colname):
        # 1-D numpy array of data we loaded application with
        orig_range = get_base_range(colname)
        colspan = orig_range['datamax'] - orig_range['datamin']

        # User filtered data from GUI
        live_data = get_column_data(colname)
        live_min = numpy.min(live_data)
        live_max = numpy.max(live_data)

        ratio = {}
        ratio['min'] = (live_min - orig_range['datamin']) / colspan
        ratio['max'] = (live_max - orig_range['datamin']) / colspan
        return ratio

# Presenter notes

- Normalize data range to [0 - 1] for a GUI widget
- Read data from model and GUI, return range [0 - 1]
- Incorrect calculation here could go unnoticed, far away from this function

--------------------------------------------------

# Assumptions

    !python
    # Base/starting data
    age = numpy.array([10.0, 20.0, 30.0, 40.0, 50.0])
    height = numpy.array([60.0, 66.0, 72.0, 63.0, 66.0])

    # Starting data
    >>> normalize_ranges('age')
    {'max': 1.0, 'min': 0.0}

    # Change current range, simulate user filtering data
    >>> age = numpy.array([20.0, 30.0, 40.0, 50.0])
    >>> normalize_ranges('age')
    {'max': 1.0, 'min': 0.25}

    >>> age = numpy.array([-10.0, 20.0, 30.0, 40.0, 50.0])
    >>> normalize_ranges('age')
    {'max': 1.0, 'min': -0.5}

# Presenter notes

- Negative numbers, numbers bigger than the actual data
- Clue you into where data is wrong
- Maybe it's correct data, just unexpected
- Maybe it's a specific set of data

--------------------------------------------------

# Lazy programmer

    !python
    def normalize_ranges(colname):
        orig_range = get_base_range(colname)

        # Max will always be greater than the minimum
        colspan = orig_range['datamax'] - orig_range['datamin']

        # User filtered data from GUI
        live_data = get_column_data(colname)
        live_min = numpy.min(live_data)
        live_max = numpy.max(live_data)

        ratio = {}

        # Numbers should always be positive
        ratio['min'] = (live_min - orig_range['datamin']) / colspan
        ratio['max'] = (live_max - orig_range['datamin']) / colspan

        # Should be between [0 - 1]
        return ratio

# Presenter notes

- These comments are a start, but their not executable. If we disobey them
  nothing happens.
- Too easy to go unnoticed

--------------------------------------------------

# Asserts

    !python
    assert 0.0 <= ratio['min'] <= 1.0, (
            '"%s" min (%f) not in [0-1] given (%f) colspan (%f)' % (
            colname, ratio['min'], orig_range['datamin'], colspan))

    assert 0.0 <= ratio['max'] <= 1.0, (
            '"%s" max (%f) not in [0-1] given (%f) colspan (%f)' % (
            colname, ratio['max'], orig_range['datamax'], colspan))

# Presenter notes

- Add asserts to verify we return correct answer, not that user passed in
  correct data

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

- Good messages with parameters/local state
- Invalid assumptions about environment
- Avoid unreproducible bugs

## More information leads to:

- New use cases
- Documentation oversights
- Remember our assert messages? They showed input params and our state

--------------------------------------------------

# Assert downsides

- Only available in debug mode
- Increased code noise
- No dynamic control

# Presenter Notes

- Use -O to run in optimized mode, turns off asserts for performance
- Default is debug on
- Docs say it's clear to use for debug, not production
- Can't control asserts dynamically, can't assign to __debug__

--------------------------------------------------

# Avoid this
.fx: small

    !python
    def normalize_ranges(colname):
        assert isinstance(colname, str)
        orig_range = get_base_range(colname)
        assert orig_range['datamin'] >= 0
        assert orig_range['datamax'] >= 0
        assert orig_range['datamin'] <= orig_range['datamax']
        colspan = orig_range['datamax'] - orig_range['datamin']
        assert colspan >= 0, 'Colspan (%f) is negative' % (colspan)

        live_data = get_column_data(colname)
        assert len(live_data), 'Empty live data'
        live_min = numpy.min(live_data)
        live_max = numpy.max(live_data)

        ratio = {}
        ratio['min'] = (live_min - orig_range['datamin']) / colspan
        ratio['max'] = (live_max - orig_range['datamin']) / colspan

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
